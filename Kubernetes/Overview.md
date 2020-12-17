# 1.Overview

Kubernetes (hay K8s hoặc "kube") là một công cụ quản lý container mã nguồn mở được tổ chức bởi Cloud Native Computing Foundation (CNCF).

Kubernetes cho khả năng triển khai tự động, scaling và triển khai ứng dụng dưới dạng container hay còn gọi là **Container orchestration engine**. Nó loại bỏ rất nhiều các quy trình thủ công liên quan đến việc triển khai và mở rộng các containerized applications.

## Các chức năng của Kubernetes.

  - Continues development, integration and deployment.
  - Containerized infrastructure.
  - Application-centric management.
  - Auto-scalable infrastructure
  - Environment consistency across development testing and production
  - Loosely coupled infrastructure, where each component can act as a separate unit.
  - Higher density of resource utilization.
  - Predictable infrastructure which is going to be created.

Một trong những chức năng chính của Kubernetes là nó có thể chạy ứng dụng trên các cụm máy vật lý, máy ảo hoặc cloud. **Điều này giúp chuyển cơ sở hạ tầng tập trung vào máy chủ (host-centric infrastructure) sang cơ sở hạ tầng tập trung vào container (container-centric infrastructure).

## Thuật ngữ cơ bản.

**Control plane:** Tập hợp các tiến trình điều khiển các node Kubernetes. Đây là nơi bắt nguồn tất cả các nhiệm nhiệm vụ được giao.

**Nodes:** Các máy này thực hiện những nhiệm vụ được giao bởi **control plane**.

**Pod**: Pod là khái niệm cơ bản và quan trọng nhất trên Kubernetes. Bản thân Pod có thể chứa 1 hoặc nhiều hơn 1 container. Pod chính là nơi ứng dụng được chạy trong đó. Pod là các tiến trình nằm trên các Worker Node. Bản thân Pod có tài nguyên riêng về file system, cpu, ram, volumes, địa chỉ network…

**Replicas Controller**: Là thành phần quản trị bản sao của Pod, giúp nhân bản hoặc giảm số lượng Pod.

**Service**: Là phần mạng (network) của Kubernetes giúp cho các Pod gọi nhau ổn định hơn, hoặc để Load Balancing giữa nhiều bản sao của Pod, và có thể dùng để dẫn traffic từ người dùng vào ứng dụng (Pod), giúp người dùng có thể sử dụng được ứng dụng.

**Label**: Label ra đời để phân loại và quản lý Pod,. Ví dụ chúng ta có thể đánh nhãn các Pod chạy ở theo chức năng frontend, backend, chạy ở môi trường dev, qc, uat, production…

**Kubelet**: Là service chạy trên các node, đọc các bản kê khai container và đảm bảo các container xác định được khởi động và chạy.

**Kubectl**: Tool quản trị Kubernetes, được cài đặt trên các máy trạm, cho phép các lập trình viên đẩy các ứng dụng mô tả triển khai vào cụm Kubernetes, cũng như là cho phép các quản trị viên có thể quản trị được cụm Kubernetes.

![](https://i.imgur.com/jYR1KSZ.png)
