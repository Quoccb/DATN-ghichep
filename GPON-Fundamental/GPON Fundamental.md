# GPON Fundamentals

GPON là viết tắt của Gigabit Passive Optical Networks. Không chỉ mỗi Ethernet, GPON có thể vận chuyển cả lưu lượng ATM và TDM (PSTN, ISDN, E1 và E3). Mạng GPON chủ yếu bao gồm hai thiết bị truyền dẫn chủ động (active) là Optical Line Termination (OLT) và Optical Network Unit (ONU) hoặc Optical Network Termination (ONT). GPIN hỗ trợ các dịch vụ triple-play (Dịch vụ Triple-Play là một loại hình dịch vụ tích hợp 3 trong 1: dịch vụ thoại, dữ liệu và Video được tích hợp trên nền IP), high-bandwidth, khoảng cách xa (lên tới 20km), v.v.

![GPON](https://i.imgur.com/dGUewoi.png)

### Components of GPON

1. OLT (Optical Line Terminal)

    OLT là một thiết bị phần cứng điểm cuối đặt tại Central Office trong mạng quang thụ động (PON). OLT chứa một đơn vị xử lý trung tâm, một gateway router, các card Voice Gateway đường lên và các card mạng quang thụ động. Chức năng chính của OLT là điều chỉnh lưu lượng (voice/data/video) vào lớp transport của PON. Nó có thể truyền một tín hiệu dữ liệu tới nhiều người dùng ở bước sóng 1490nm. Tín hiệu đó có thể chia lên đến 128 ONT trong phạm vi 12.5 dặm bằng cách sử dụng các bộ chia quang.

2. Optical Splitter

    Bộ chia quang chia công suất tín hiệu. Có nghĩa là, mỗi liên kết sợi quang đi vào bộ chia quang có thể chia thành một số lượng nhất định sợi quang ở đầu ra bộ chia quang. Thông thường, ba cấp sợi quang trở lên tương ứng với hai hoặc nhiều cấp bộ chia. Điều này cho phép chia sẻ mỗi sợi quang cho nhiều người dùng. Bộ chia quang thụ động có các tính chất của dải bước sóng hoạt động rộng, kích thước tối thiểu, độ tin cậy cao và hỗ trợ chính sách bảo vệ và khả năng tồn tại của mạng.

3. Optical Network Unit (ONU)

    ONU chuyển các tín hiệu quang được truyền qua sợi quang thành các tín hiệu điện sau đó gửi tới từng thuê bao. Nói chung, có một khoảng cách hoặc mạng truy cập khác giữa ONU và cơ sở của người dùng cuối. Hơn nữa, ONU có thể gửi, tổng hợp và *groom* các loại dữ liệu khác nhau đến từ khách hàng và gửi ngược về OLT (Upstream). Grooming là quá trình tối ưu hóa và tổ chức lại luồng dữ liệu để nó được phân phối hiệu quả hơn. OLT hỗ trợ phân bổ băng thông cho phép phân phối dữ liệu (thường đến từng đợt từ phía khách hàng) trôi chảy đến OLT. ONU có thể được kết nối bằng nhiều cách và bằng nhiều loại cáp như cáp xoắn đôi, cáp đồng trục, cáp quang hoặc Wi-Fi.

4. ONT (Optical Network Terminal)
    ONU và ONT về cơ bản là cùng một thiết bị - ONT được đặt ở cơ sở của khách hàng còn ONU được đặt bên ngoài nhà. ONU có thể làm việc trong các điều kiện nhiệt độ, thời tiết khách nhau. Nó phải chống nước, gió và các yếu tố phá hoại khác. ONU thường giao tiếp với một ONT ( có thể là một hộp riêng biệt kết nối PON tới bộ TV, điện thoại, máy tính hoặc một một bộ định tuyến không dây)

    ONT được triển khai tại cơ sở của khách hàng. Nó được kết nối tới OLT bằng sợi quang và không có phần tử chủ động nào có mặt trong liên kết. Trong GPON, bộ thu phát trên ONT là kết nối vật lý giữa cơ sở khách hàng và Central Office OLT.


## GPON principle
GPON áp dụng kỹ thuật ghép kênh phân chia theo bước sóng - Wavelength Division Multiplexing (WDM) tạo điều kiện cho giao tiếp hai chiều qua một sợi quang.

![GPON principal](https://i.imgur.com/jmnS2mt.png)

Để tách các tín hiệu upstream/downstream của nhiều người dùng qua một sợi quang, GPON sử dụng hai cơ chế ghép kênh:
- Downtream: các gói dữ liệu được truyền broadcast.
- Upstream: các gói dữ liệu được truyền theo kỹ thuật TDMA.

![Broadcast mode](https://i.imgur.com/20BaYQP.png)

![TDMA mode](https://i.imgur.com/ppBOPxb.png)

## Quá trình phát triển của chuẩn PON

![GPON progress](https://i.imgur.com/DboO2UL.png)

# Kiến trúc của mạng truy nhập quang (Optical Access Network)

![FTHx](https://i.imgur.com/0ifnr1C.png)

![GPON Architecture](https://i.imgur.com/PzvvDyk.png)

![](https://i.imgur.com/GspxelA.png)
