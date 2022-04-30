# Wi-Fi



## Beacon

Beacon-Interval(信标间隔)，这个值变大，有助于client端省电。这个值变小，有助于提高client端连接速度。降低了基地台的buffer frame负载。一般预设为100mS。以Beacons 封包发送SSID的速率是1Mbit/S.

Listen-Interval(STA接收Beacon的周期)，AP广播Beacon的周期为Beacon-Interval，STA可以自由选择Beacon-Interval整数倍作为自己的Listen-Interval，比如10。

STA每隔Listen-Interval接收Beacon并解码其中的TIM，如果TIM 指示没有数据缓存，STA 就可以立刻转入Doze状态，如果TIM 指示其有数据缓存，STA 就要向AP 发一个竞选控制包Poll，AP 在收到Poll 后就可以向该Poll 的源STA 发送一个为它缓存的数据包。

## DTIM

每一个Beacon的帧中都有一个TIM(traffic indication message)信息元素，它主要用来由AP通告它管辖下的哪个STA有信息现在缓存在AP中，而在TIM中包含一个 Bitmap control 字段，它最大是251个字节，每一位映射一个STA，当为1时表示该位对应的STA有信息在AP中。

STA收到与自己关联的TIM就要发送PS-POLL帧来与AP取来联系并取得它的缓存帧，标准的TIM中仅仅指示AP缓存的单播信息。

DTIM(Delivery Traffic Indication Message)是TIM的特殊情况，当发送几个TIM之后，就要发送一个DTIM，其除了缓存单播信息，也同时指示AP缓存的组播或广播信息，一旦AP发送了DTIM, STA就必须处于清醒，因为广播或组播无重发机制，不醒来数据就收不到了。

DTIM用于AP传统节电模式中，多点的应用，即由AP通过设置DTIM的间隔（缺省是一个beacon时间，100ms），根据这个间隔发送组播流量。

也就是说DTIM里面会指示是否有组播数据，也会指示是否有单播数据。

如果beacon包含的DTIM里面有组播数据，也包含了单播的数据。STA会马上唤醒，接受组播数据，接受完成之后，会继续接收单播数据。


## Multicast

根据协议，Broadcast 和 Multicast(组播) 在DTIM的时候AP会发送给STA。DTIM在AP中的设置一般是一倍的TIM。

当DTIM增加的时候会更加省电，因为出于PS模式下的STA醒来的次数变少了，但是这也会导致某些应用的延时加大。

在以太网数据帧头中会需要指定发送以及接受设备的MAC地址，以确定该数据包的来源与去向，广播时接收方的MAC地址为0xFFFFFFFFFFFF，单播时接收方的MAC地址为对端MAC地址，而组播时，接收方的MAC地址则与组地址之间有一个映射关系，而WiFi组播配网正是利用了这个组地址与MAC地址的映射。判断一个MAC是否为组播MAC的依据是MAC地址的第一个字节的bit0是否为１。

