# Docker - Images

Trong Docker, tất cả mọi thứ đều dựa trên **Images**. Một Image là sự kết hợp giữa một file hệ thống và các thông số.

Ví dụ một lệnh trong Docker:

    $ docker run hello-world

Trong đó:
  - **Docker** dùng để cho hệ điều hành biết là mình đang muốn chạy lệnh trên Docker.
  - **run** là lệnh Docker để tạo một **instance** của một **image**, **instance** chính là **container**.
  - **hello-world** là tên của một image mà ta muốn tạo container.

## Một số lệnh Docker.

### Hiển thị Docker Image

Để xem danh sách Docker Image trên hệ thống, dùng lênh sau:

    $ docker images

Kết quả:


Trong đó ta thấy các attribute của mỗi image:
  - **TAG** - Version của Image.
  - **Image ID** - Định danh duy nhất cho image .
  - **Created** - Số ngày kể từ khi image được khởi tạo.
  - **Virtual Size** - Size của image.

### Tải Docker Image

Image có thể được tải trực tiếp từ Docker Hub bằng lệnh **run** nếu Image chưa có trên hệ thống.

### Removing Docker Image.

Docker Image trên hệ thống có thể bị xóa bằng lệnh **rmi**.

    docker rmi <ImageID>

### Lệnh *Docker images -q*

    sudo docker images -q

Lệnh này sẽ chỉ trả về các ID của Image.

### *docker inspect*

Lệnh này được dùng để xem chi tiết một image hoặc một container.

    sudo docker inspect Repository
