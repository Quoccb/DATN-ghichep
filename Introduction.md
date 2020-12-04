# What is OpenStack?
OpenStack là một bộ công cụ phần mềm xây dựng và quản lý các nền tảng quản lý điện toán đám mây (cloud computing) cho *public cloud* và *private cloud*. Được hỗ trợ bởi những công ty lớn nhất về phát triển phần mềm và hosting cùng một cộng đồng với hàng ngàn thành viên, nhiều người nghĩa rằng OpenStack là tương lai của điện toán đám mây. OpenStack được quản lý bởi [OpenStack Foundation](https://openinfra.dev/about/), một tổ chức phi lợi nhuận giám sát cả quá trình phát triển và xây dựng cộng đồng xung quanh dự án.

Đặc biệt OpenStack là một phần mềm mã nguồn mở, có nghĩa là bất cứ ai đều có thể truy cập vào mã nguồn, thực hiện bất kỳ thay đổi hay chỉnh sửa nào họ cần và tự do chia sẻ những thay đổi này với cộng đồng nói chung. Điều này cũng có nghĩa là OpenStack được xây dựng, đóng góp từ cộng đồng hàng ngàn developer trên toàn thế giới để phát triển sản phẩm mạnh mẽ nhất, an toàn nhất có thể.

# OpenStack được sử dụng thể nào trong môi trường Cloud

Mục đích của Cloud là cung cấp điện toán cho người dùng cuối trong môi trường từ xa nơi mà các phần mềm thực sự chạy như một dịch vụ trên các máy chủ đáng tin cậy và có thể mở rộng thay vì chạy trên máy tính của người dùng cuối. Định nghĩa theo NIST:

  ``"Cloud Computing  là mô hình cho phép truy cập qua mạng để lựa chọn và sử dụng tài nguyên  có thể được tính toán (ví dụ: mạng, máy chủ, lưu trữ, ứng dụng và dịch vụ) theo nhu cầu một cách thuận tiện và nhanh chóng; đồng thời cho phép kết thúc sử dụng dịch vụ, giải phóng tài nguyên dễ dàng, giảm thiểu các giao tiếp với nhà cung cấp”"``

Cloud Computing có **5 đặc tính**, **4 mô hình dịch vụ** và **3 mô hình triển khai**.

**5 đặc điểm:**
  - Khả năng thu hồi và cấp phát tài nguyên(Rapid elasticity)
  - Truy nhập qua các chuẩn mạng (Broad network access)
  - Dịch vụ sử dụng đo đếm được (Measured service,) hay là chi trả theo mức độ sử dụng (pay as you go.)
  - Khả năng tự phục vụ (On-demand self-service).
  - Chia sẻ tài nguyên (Resource pooling).

**4 mô hình dịch vụ (mô hình sản phẩm)**
  - Public Cloud: Đám mây công cộng (là các dịch vụ trên nền tảng Cloud Computing để cho các cá nhân và tổ chức thuê, họ dùng chung tài nguyên).
  - Private Cloud: Đám mây riêng (dùng trong một doanh nghiệp và không chia sẻ với người dùng ngoài doanh nghiệp đó)
  - Community Cloud: Đám mây cộng đồng (là các dịch vụ trên nền tảng Cloud computing do các công ty cùng hợp tác xây dựng và cung cấp các dịch vụ cho cộng đồng. Tôi cũng chưa rõ FB có phải là một dạng này không, cần xác nhận lại.
  - Hybrid Cloud : Là mô hình kết hợp (lai) giữa các mô hình Public Cloud và Private Cloud (không rõ có Community Cloud nữa không … :D)

**3 mô hình triển khai: tức là triển khai Cloud Computing để cung cấp:**
  - Hạ tầng như một dịch vụ (Infrastructure as a Service)
  - Nền tảng như một dịch vụ (Platform as a Service)
  - Phần mềm như một dịch vụ (Software as a Service)

OpenStack thuộc loại thứ nhất và được xem như Infrastructure as a Service (IaaS). Cung cấp hạ tầng có nghĩa là OpenStack giúp người dùng dễ dàng thêm instance mới một cách nhanh chóng để các thành phần Cloud khác có thể chạy trên đó. Thông thường, hạ tầng sau đó chạy một "platform" mà trên đó nhà phát triển có thể tạo ra các ứng dụng phần mềm được phân phối đến người dùng cuối.
