# Introduction to SDN OpenDayLight


OpenDayLight là một controler/framework SDN có mã nguồn mở, được tổ chức bởi Linux Foundation. Đây là một controller SDN (mã nguồn mở) rất phổ biến hiện nay.

Một trong những giao thức Southbound Interface mà Open hỗ trợ là OpenFlow. Để test OpenDayLight, ta cần một vài switch hỗ trợ OpenFlow.

Nếu không có những phần cứng hỗ trợ OpenFlow ta có thể sử dụng Mininet thay thế để phục vụ học tập, nghiên cứu.

Mininet cho phép ta chạy một mạng ảo trên chính máy tính của mình với những thiết bị hỗ trợ OpenFlow.

Dưới đây là mô hình mạng đơn giản ta sẽ xây dựng.

![](https://i.imgur.com/1TWkSXZ.png)

Mô hình mạng gồm có một SDN controller là OpenDayLight, hai OpenFlow Switch được điều khiển bởi SDN controller và 2 host, mỗi host kết nối với một Switch.

Để thiết lập mạng này ta sẽ sử dụng 2 máy ảo như sau:

![](https://i.imgur.com/cGK30zV.png)

Một máy ảo là Mininet Server với 2 interface. eth0 interface sử dụng DHCP client, ta sử dụng interface này để SSH vào server. interface còn lại là eth1 sẽ được các switch ảo sử dụng để giao tiếp với OpenDayLight controller.

Máy ảo còn lại là OpenDayLight controller, cũng có 2 interface. ens160 interface sẽ được sử dụng để SSH vào box và để truy nhập GUI/API. Interface còn lại là ens192 được dùng giao tiếp với các switch ảo trên Mininet.

# 1. Cài đặt OpenDayLight

## 1.1. Network Interface

Mặc định trên máy ảo sẽ có một network interface được kích hoạt sẵn (interface ens33) , ta sẽ dùng nó cho DHCP client nên ta cần phải tự thêm một network interface nữa.

![](https://i.imgur.com/jHQYwjZ.png)

Để cấu hình network interface mới ta thêm vào file */etc/network/interfaces* đoạn mã sau:

```
# Second interface
auto ens38
iface ens38 inet static
address 192.168.1.254
netmask 255.255.255.0
```

![](https://i.imgur.com/fk24zz0.png)

Sau đó dùng lệnh `sudo ifup ens38` để kích hoạt interface.

## 1.2. Java

OpenDayLight là một chương trình Java nên ta cần cài đặt runtime:

    $ sudo apt-get install default-jre-headless
<br>

    $ echo 'export JAVA_HOME=/usr/lib/jvm/default-java' >> ~/.bashrc
<br>

    $ source ~/.bashrc

## 1.3. OpenDayLight

Có thể Download OpenDayLight bản mới nhất [tại đây](https://docs.opendaylight.org/en/latest/downloads.html)

    $ wget https://nexus.opendaylight.org/content/repositories/opendaylight.release/org/opendaylight/integration/karaf/0.13.1/karaf-0.13.1.zip

Sau khi tải về file zip ta unzip nó:

    $ unzip karaf-0.13.1.zip

Bây giờ ta có thể khởi động controller.

    $ cd karaf-0.13.1/
    $ ./bin/karaf

![](https://i.imgur.com/n6FwXuT.png)

OpenDayLight sử dụng một container karaf. Đây là công nghệ của Apache cho phép chạy mọi thứ từ một folder duy nhất. File ZIP mà ta đã download chứa mọi thứ, gồm phần mềm OpenDayLight và cả Apache webserver cùng một số thứ khác. Không cần thiết phải tự cài đặt một webserver.

Controller đã đi kèm với một số tính năng cơ bản, nhưng nếu muốn làm một vài điều hữu dụng ta cần phải thêm một số tính năng bổ sung. Ta sẽ thử sử dụng GUI, RESTCONF API và một số chức năng chuyển mạch cơ bản L2 để học địa chỉ MAC. Ta cần phải cài đặt những chức năng sau.

    opendaylight-user@root>feature:install odl-restconf odl-l2switch-switch odl-mdsal-apidocs odl-dlux-all


Bây giờ ta vào Browser truy cập vào URL:

    http://192.168.1.254:8181/index.html#login

*Trong đó 192.168.1.254 là địa chỉ IP của OpenDayLight.*

![](https://i.imgur.com/0xcRHrU.png)

**Username:** admin
<br>**Password:** admin

Ở máy ảo Mininet ta thiết lập một mô hình mạng bao gồm:
  - Hai switch ảo hỗ trợ Openflow
  - Hai host ảo, mỗi host nối với một Switch.
  - Một SDN controller là OpenDayLight.

Sử dụng lệnh sau:

    $ sudo mn --topo linear,2 --mac --controller=remote,ip=192.168.1.254,port=6633 --switch ovs,protocols=OpenFlow10

Reload lại màn hình controll trên OpenDayLight GUI ta sẽ có:

![](https://i.imgur.com/RU91mng.png)

Các node trên mạng đã có thể ping đến nhau.

Sau khi dùng lệnh `pingall` trên Mininet, reload lại màn hình controll ta có mô hình mạng:

![](https://i.imgur.com/NRpsyoc.png)
