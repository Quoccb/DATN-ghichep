Bắt đầu cài đặt Docker trên Ubuntu. Sử dụng VMware để thiết lập một máy ảo Linux với một user tên là quoc được cấp quyền truy nhập như root.

![](https://i.imgur.com/1uq9IuP.png)

Cài đặt Docker cần các bước sau:

**Bước 1**: Trước khi cài đặt Docker, đầu tiên cần đảm bảo rằng Linux kernel đang chạy đúng phiên bản. Docker chỉ được thiết kế để chạy trên Linux kernel phiên bản 3.8 trở lên. Kiểm tra bằng lệnh *uname* - trả về thông tin về hệ thống Linux.

    uname -a

**a** - được dùng để đảm bảo thông tin hệ thống được trả về.

Câu lệnh sẽ trả về những thông tin sau:

  - kernel name
  - node name
  - kernel release
  - kernel version
  - machine
  - processor
  - hardware platform
  - operating system

Ví dụ:

![](https://i.imgur.com/JAMSBrh.png)

Nhìn output có thể thấy Linux kernel đang ở phiên bản 4.4.0-142 cao hơn 3.8.

**Bước 2**: Cần cập nhật OS với những packages mới nhất bằng lệnh *apt-get*.

Lệnh này sẽ kết nối tới internet và tải các package hệ thông mới nhất cho Ubuntu.

    sudo apt-get update

![](https://i.imgur.com/i1Pnewi.png)

**Bước 3**: Bước tiếp theo là cài đặt những chứng chỉ cần thiết để có thể làm việc với trang Docker khi tải xuống những package cho Docker. Có thể dùng lệnh sau:

    sudo apt-get install apt-transport-https ca-certificates

![](https://i.imgur.com/XwCoTiP.png)

**Bước 4**: Bước tiếp theo là thêm khóa GPG mới. Khóa này để đảm bảo tất cả dữ liệu được mã hóa khi tải những package cho Docker.

    $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

![](https://i.imgur.com/kyGFch5.png)

Kiểm tra lại một chút:

![](https://i.imgur.com/6naLZ82.png)

**Bước 5** : Thêm Docker repository vào APT sources:

    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"

**Bước 6** : Cài đặt docker-ce:

Cập nhật cơ sở dữ liệu package với các gói Docker từ repo mới adđ:

    $ sudo apt update

Sau đó cài đặt Docker:

    $ sudo apt install docker-ce

Check:

    $ sudo docker version

![](https://i.imgur.com/ssOpyxY.png)
