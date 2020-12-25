# Introduction to SDN (Software Defined Networking)

# Mục lục

- [1. Mạng truyền thống](#1)
  - [1.1. Controll Plane](#2)
  - [1.2. Data Plane](#3)
  - [1.3. Management Plane](#4)
- [2. Hạn chế của mạng truyền thống](#5)
- [3.SDN (Software Defined Networking)](#6)
  - [Southbound Interface](#7)
  - [Northbound Interface](#8)
  - [REST API](#9)

<a name='1' ></a>
## 1. Mạng truyền thống
Đối với mạng truyền thống, ta có các thiết bị mạng đặc trưng như *Router, Switch và Firewall*, chúng được sử dụng cho các tác vụ cụ thể.

Những thiết bị mạng này được bán từ các nhà cung cấp mạng như **Cisco** và thường sử dụng phần cứng độc quyền. Hầu hết những thiết bị này được cấu hình chủ yếu qua CLI, tuy nhiên vẫn có vài sản phẩm GUI như CCP (Cisco Configuration Protocol) cho router hoặc ASDM cho Cisco ASA firewall.

Ví dụ, một router có các chức năng khác nhau phải thực hiện. Để chuyển tiếp một gói tin IP, router cần thực hiện những việc sau:
  - Nó phải kiểm tra địa chỉ IP đích trong bảng định tuyến để biết nó cần chuyển tiếp gói tin IP đi đâu.
  - Cần có các giao thức định tuyến như OSPF, EIGRP hay BGP để tìm hiểu mạng đã được cài đặt trong bảng định tuyến.
  - Nó phải sử dụng giao thức ARP để xác định địa chỉ MAC đích của *next hop* và thay đổi địa chỉ MAC đích trong khung Ethernet.
  - TTL (Time To Live) trong gói tin IP phải giảm 1 và giá trị checksum trong IP header cần phải tính lại.
  - Giá trị Checksum trong khung Ethernet cũng phải tính toán lại.

Tất cả các tác vụ khác nhau trên được phân biệt bằng các **plane** khác nhau. Có 3 **plane**:
  - **control plane**
  - **data plane**
  - **management plane**

  ![](https://i.imgur.com/9wXu3TP.png)

<a name='2' ></a>
### 1.1. Control Plane

**Control Plane** có nhiệm vụ trao đổi thông tin định tuyến, xây dựng bảng ARP, v.v. Dưới đây là một số tác vụ được thực hiện bởi **control plane**:

  - Học địa chỉ MAC để xây dựng bảng địa chỉ MAC.
  - Chạy STP để tạo một cấu trúc liên kết không có vòng lặp.
  - Xây dựng bảng ARP.
  - Chạy các giao thức định tuyến như OSPF, EIGRP, BGP và xây dựng bảng định tuyến.

<a name='3' ></a>
### 1.2. Data Plane

**Data Plane** có nhiệm vụ chuyển tiếp lưu lượng dựa trên thông tin mà **control plane** cung cấp. Dưới đây là một số tác vụ **data plane** cần thực hiện:

  - Mở và đóng gói các gói tin.
  - Thêm và xóa các header như 802.1Q header.
  - Đối chiếu các địa chỉ MAC để chuyển tiếp gói tin.
  - Đối chiếu IP đích trong bảng định tuyến.
  - Thay đổi địa chỉ nguồn và địa chỉ đích khi sử dụng NAT.
  - Dropping traffic because of access-lists.

Các tác vụ của **data plane** phải được thực hiện nhanh nhất có thể, đó là lý do vì sao các việc chuyển tiếp lưu lượng được thực hiện bởi phần cứng chuyên dụng như ASIC và bảng TCAM.

<a name='4' ></a>
### 1.3. Management Plane
**Management plane** được sử dụng cho truy nhập và quản lý các thiết bị mạng. Ví dụ, truy nhập thiết bị qua **telnet**, **SSH** hoặc **console port**.

Khi nói về SDN, **control** và **data plane** là quan trọng và cần phải lưu ý nhất. Minh họa dưới đây giúp hình dung rõ hơn về **control** và **data plane**:

![](https://i.imgur.com/5UKKDoH.png)

![](https://i.imgur.com/paVqwXX.png)

Có thể thấy rằng **control plane** là nơi thực hiện những giao thức như OSPF, EIGRP và một số định tuyến tĩnh. Tuyến đường tốt nhất sẽ được thiết lập vào bảng định tuyến. Router cũng phải xây dựng một bảng khác là bảng ARP.

Thông tin từ bảng định tuyến và bảng ARP sau đó được dùng để xây dựng bảng chuyển tiếp (Forwarding table). Khi router nhận một gói tin IP, nó sẽ có thể chuyển tiếp gói tin một cách nhanh chóng nhờ Forwarding Table đã được xây dựng trước đó.

<a name='5' ></a>
## 2. Hạn chế của mạng truyền thống.

Kiến trúc mạng truyền thống như mô tả ở trên đã được xây dựng và phát triển trong hàng chục năm qua nên không có vấn đề gì "sai" đối với mạngt truyền thống cả. Vấn đề ở đây là vấn đề kinh tế, những thách thức kinh tế hiện nay đang đòi hỏi những giải pháp khác nhau.

Ví dụ:

![](https://i.imgur.com/dC1OV4M.png)

Minh họa ở trên là cơ sở hạ tầng mạng của trung tâm dữ liệu của một công ty. Ở dưới cùng, ta thấy một máy chủ VMware ESXi với một số máy ảo (VM). Máy chủ này được kết nối tới một số Switch trong lớn access và lớp aggregation. Ta cũng thấy hai ASA bảo vệ máy chủ và hai Router để truy cập mạng bên ngoài. Trên cùng, có một Router khác với một host.

Giả sử rằng công ty này có một yêu cầu kinh doanh cần một ứng dụng mới yêu cầu 4 máy ảo mới để có thể cài đặt trên máy chủ VMware. Vì lý do bảo mật, mỗi máy ảo phải nằm trong một VLAN khác nhau. Người dùng H1 ở R3 phải có khả năng truy nhập ứng dụng chạy trên những máy ảo này.

Để thực hiện những yêu cầu trên, cần phải cấu hình trên mạng những cấu hình sau:

  - Các VLAN phải được tạo trên tất cả Switch.
  - Phải cấu hình một Root Bridge cho các VLAN mới.
  - Phải gán 4 subnet mới, mỗi VLAN một subnet.
  - Phải tạo sub-interface mới với địa chỉ IP trên các Switch.
  - Cần cấu hình VRRP hay HSRP trên các Switch cho VLAN mới.
  - Phải cấu hình Firewall để cấp phép truy nhập tới các application/subnet mới.
  - Phải quảng bá các subnet mới trong giao thức định tuyến trên Switch, Router và Firewall.

Mặc dù có những công cụ tự động hóa mạng hỗ trợ, ta thường dùng CLI để cấu hình tất cả các thiết bị này, từng cái một. Quá trình này con người phải làm thủ công, chậm chạp và nhàm chán. Mặc dù mở một máy ảo chỉ mất vài phút nhưng cấu hình mạng lại mất vài giờ. Hơn nữa những thay đổi này thường phải thực hiện trong thời gian bảo trì chứ không phải trong giờ làm.

Ảo hóa máy chủ là một trong những lý do tại sao các doanh nghiệp đang tìm kiếm thứ gì đó giúp tăng tốc quá trình ở trên. Trước khi ảo hóa, chúng ta từng có một máy chủ vật lý với một hệ điều hành duy nhất. Ngày nay chúng ta có nhiều máy chủ vật lý với hàng trăm máy ảo.

Những máy ảo này có khả năng di chuyển tự động từ máy chủ vật lý này sang máy chủ vật lý khác.

Xu hướng bay giờ là mọi thứ phải được ảo hóa nên ảo hóa mạng cũng là xu thế tự nhiên. Các công ty lớn như Cisco từng chỉ bán phần cứng độc quyền giờ cũng cung cấp các router ảo, ASAs, Wireless LAN controller, v.v. có thể chạy trên máy chủ VMware.

<a name='6' ></a>
## 3. SDN (Software Defined Networking)

Giống như "cloud" hot mấy năm trước, mọi tổ chức hoặc nhà cung cấp đều có những định nghĩa khác nhau về SDN và cung cấp những sản phẩm khác nhau.

Mạng truyền thống sử dụng mô hình phân tán (**distributed model**) cho **control plane**. Những giao thức như ARP, STP, OSPF, EIGRP, BGP, ... chạy độc lập trên mỗi thiết bị mạng. Những thiết bị mạng này giao tiếp với nhau nhưng không có thiết bị trung tâm nào có cái nhìn tổng quát hay điều khiển toàn bộ mạng.

WLC (wireless LAN controller) là một ngoại lệ. Khi cấu hình mạng không giây, ta cấu hình mọi thứ trên WLC rồi WLC sẽ điều khiển và cấu hình các điểm truy nhập. Ta không cần phải cấu hình cho mỗi điểm  truy nhập nữa, WLC làm tất.

Với SDN, ta sử dụng một bộ điều khiển trung tâm (**Central Controller**) cho control plane. Tùy thuộc vào giải pháp của nhà cung cấp, điều này có nghĩa rằng bộ điều khiển SDN tiếp quản hoàn toàn control plane hay nó chỉ có thông tin chi tiết trong control plane của tất cả thiết bị trong mạng. Bộ điều khiển SDN có thể là thiết bị phần cứng vật lý hoặc máy ảo.

Minh họa dưới đây giúp hình dung rõ hơn:

![](https://i.imgur.com/fbUUj1X.png)

Ta có thể thấy SDN controller phụ trách hoàn toàn control plane. Các Switch bây giờ không còn **thông minh** nữa vì chỉ còn lại **data plane**, không **control plane**. SDN controller có nhiệm vụ cung cấp cho **data plane** của những Switch này các thông tin từ **control plane** của nó.

Có một số ưu điểm và nhược điểm giữa control plane tập trung và control plane phân tán. Một trong những ưu điểm của bộ điều khiển tập trung là có thể cấu hình toàn bộ mạng từ một thiết bị duy nhất. Bộ điều khiển này có toàn quyền truy nhập và thông tin chi tiết về mọi thứ đang diễn ra trong mạng.

![](https://i.imgur.com/gLVDUNq.png)

SDN controller có hai giao diện gọi là **northbound interface (NBI)** và **southbound interface (SBI)**.

<a name='7' ></a>
### Southbound Interface

SDN controller phải giao tiếp với các thiết bị mạng để lập trình **data plane**. Điều này được thực hiện thông qua southbound interface. Đây không phải là giao diện vật lý mà là giao diện mềm (software interface), thường là một API (Application Programming Interface).

Một API là một giao diện phần mềm cho phép một ứng dụng cấp phép truy nhập vào ứng dụng khác bằng các hàm và cấu trúc dữ liệu được định nghĩa trước.

Một số giao diện southbound interface phổ biến là:

  - OpenFlow: Đây có lẽ là SBI phổ biến nhất thời điểm hiện tại, nó là một giao thức mã nguồn mở từ [Open Networking Foundation](https://opennetworking.org/). Có khá nhiều thiết bị mạng và SDN controller hỗ trợ OpenFlow.
  - Cisco OpFlex: Đây là đáp trả của Cisco cho OpenFlow. Nó cũng là một giao thức mã nguồn mở đã được đệ trình lên IETF để chuẩn hóa.
  - CLI: Cisco đề xuất APIC-EM, là một giải pháp SDN cho thế hệ router và switch hiện tại. Nó sử dụng các giao thức khả dụng trên thế hệ phần cứng hiện tại như telnet, SSH và SNMP.

<a name='8' ></a>
### Northbound Interface

NBI được sử dụng để truy nhập vào chính SDN controller. Điều này cho phép quản trị viên của mạng truy nhập vào SDN để cấu hình nó hoặc truy xuất thông tin từ nó. Điều này có thể được hoàn thành thông qua một GUI nhưng nó cũng cung cấp một API cho phép những ứng dụng khác truy nhập tới SDN controller. Bạn có thể sử dụng điều này để viết những scrip và tự động hóa việc quản trị mạng của bạn.

  - Liệt kê thông tin từ tất cả các thiết bị trong mạng.
  - Hiển thị trạng thái của tất cả các giao diện vật lý trong mạng.
  - Thêm một VLAN mới trong toàn bộ switch.
  - Hiển thị cấu trúc liên kết (topology) của toàn mạng.
  - Tự động cấu hình địa chỉ IP, định tuyến và access-list khi một máy ảo mới được tạo.

Dưới đây là minh họa giúp mô phỏng:

![](https://i.imgur.com/rXdnPte.png)

Qua API, nhiều phần mềm có thể truy
 nhập SDN controller.
  - Một người dùng đang sử dụng GUI để truy xuất thông tin về mạng từ SDN Controller. GUI đang sử dụng API
  - Những Script được viết bằng Java hoặc Python có thể sử dụng API để truy xuất thông tin từ SDN Controller hoặc cấu hình mạng.
  - Những ứng dụng khác cũng có thể truy nhập SDN Controller. Có thể là một ứng dụng tự động cấu hình mạng khi một máy ảo mới được tạo trên máy chủ VMware ESXi.

<a name='9' ></a>
### REST API

Như đã nói ở trên, giao diện northbound và southbound đều sử dụng API. Vậy API là gì?. SDN Controller thường sử dụng một REST API (Representational State Transfer).

REST API sử dụng gói tin HTTP để gửi và nhận thông tin giữa SDN Controller và ứng dụng khác. Nó sử dụng những gói tin HTTP tương như khi ta duyệt một trang web trên Internet hay khi ta nhập một biểu mẫu online.
   - HTTP GET: Dùng khi cần truy xuất thông tin.
   - HTTP POST/PUT: Dùng khi muốn upload hay update thông tin.

Tương tự như duyệt web, chỉ là không phải yêu cầu một trang web hay một bức ảnh mà là yêu cầu một đối tượng cụ thể từ SDN Controller ví dụ như một danh sách với tất cả VLAN trong mạng.

Khi SDN Controller nhật yêu cầu HTTP GET, nó sẽ trả lời  một phản hồi HTTP GET với thông tin đã được yêu cầu. Thông tin này được phân phối dưới định dạng dữ liệu chung. Hai định dạng dữ liệu được sử dụng nhiều nhất là:
  - JSON (JavaScript Object Notation)
  - XML (eXtensible Markup Language)

Một ví dụ để dễ hình dung:

![](https://i.imgur.com/x5hWZGR.png)

Ở trên, ta có một tập lệnh python đang sử dụng HTTP GET để tìm nạp URL thông qua API:

>  https://192.168.1.1:8443/sdn/v2.0/net/nodes

URL này sẽ truy xuất một số biến có sẵn ví dụ như thông tin về tất cả các node (host) trên mạng.

Khi API nhận được điều này, nó sẽ phản hồi bằng một thông báo phản hồi HTTP GET:

![](https://i.imgur.com/I14UHru.png)

Các biến được yêu cầu sẽ sẽ được cung cấp dưới định dạng JSON như sau:

```JSON
{
	"nodes": [
		{
		"ip": "172.16.1.1",
		"mac": "fa16.3e5d.f1f4",
		"vid": 0,
		"dpid": "00:00:00:00:00:00:00:03",
		"port": 1
	}, {
		"ip": "172.16.1.2",
		"mac": "fa16.3e5d.f1f5",
		"vid": 0,
		"dpid": "00:00:00:00:00:00:00:03",
		"port": 2
	}
]
}
```

Dễ dàng đọc hiểu khối code ở trên, ta có 2 node trên mạng với địa chỉ IP, và địa chỉ MAC tương ứng.
