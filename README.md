# docker

Dưới đây là một số câu lệnh cơ bản để thực hành với Docker:

1. Xem danh sách các images đã tải xuống:

```
docker images

```

1. Tải một image từ Docker Hub:

```
docker pull ten_image

```

1. Tạo một container từ một image có sẵn:

```
docker run --name ten_container -d ten_image

```

1. Tạo một container từ Dockerfile:

```
docker build -t ten_image .
docker run --name ten_container -d ten_image

```

1. Xem danh sách các container đang chạy:

```
docker ps

```

1. Dừng container đang chạy:

```
docker stop ten_container

```

1. Xóa container:

```
docker rm ten_container

```

1. Xóa image:

```
docker rmi ten_image

```

1. Xem thông tin chi tiết về một container:

```
docker inspect ten_container

```

1. Tạo một network mới:

```
docker network create ten_network

```

1. Liên kết một container với network:

```
docker network connect ten_network ten_container

```

1. Tạo một volume mới:

```
docker volume create ten_volume

```

1. Mount volume vào container:

```
docker run -v ten_volume:/path/to/mount ten_image

```

1. Tạo và quản lý ứng dụng Docker với Docker Compose:

```
docker-compose up -d
docker-compose down

```

1. Tìm kiếm image trên Docker Hub:

```
docker search ten_image

```

Lưu ý: Bạn có thể thay đổi các tham số của các câu lệnh trên để phù hợp với nhu cầu của mình.

Tích hợp Docker vào ứng dụng ReactJS sẽ giúp bạn đóng gói ứng dụng và các phụ thuộc của nó vào một image Docker, và triển khai nó trên bất kỳ môi trường nào có Docker cài đặt. Bằng cách đó, bạn có thể đảm bảo rằng ứng dụng của bạn sẽ chạy một cách đồng nhất trên môi trường phát triển và sản phẩm.

Dưới đây là các bước cơ bản để tích hợp Docker vào ứng dụng ReactJS:

1. Tạo Dockerfile: Tạo một Dockerfile để đóng gói ứng dụng và các phụ thuộc của nó vào một image Docker. Bạn có thể bắt đầu với một Dockerfile đơn giản như sau:

```
# Sử dụng image nodejs làm base image
FROM node:latest

# Tạo thư mục app và copy nội dung của thư mục app vào
WORKDIR /app
COPY . /app

# Cài đặt các phụ thuộc của ứng dụng
RUN npm install

# Build ứng dụng
RUN npm run build

# Chạy ứng dụng
CMD [ "npm", "start" ]

```

1. Build Docker image: Chạy câu lệnh sau để build image từ Dockerfile:

```
docker build -t ten_image .

```

1. Chạy Docker container: Chạy câu lệnh sau để chạy container từ image vừa build:

```
docker run -p 3000:3000 ten_image

```

Giả sử ứng dụng của bạn chạy trên cổng 3000, và bạn muốn ánh xạ cổng 3000 trên container sang cổng 3000 trên máy chủ của bạn.

1. Kiểm tra ứng dụng: Truy cập [http://localhost:3000](http://localhost:3000/) trên trình duyệt của bạn để kiểm tra ứng dụng ReactJS của bạn đã chạy trên Docker container.

Lợi ích của việc tích hợp Docker vào ứng dụng ReactJS bao gồm:

- Dễ dàng đóng gói và triển khai ứng dụng trên bất kỳ môi trường nào có Docker cài đặt.
- Đảm bảo tính đồng nhất của ứng dụng trên các môi trường khác nhau.
- Giảm thời gian cài đặt và cấu hình môi trường phát triển cho các thành viên trong nhóm phát triển.
- Giúp giảm thiểu sự khác biệt giữa môi trường phát triển và sản phẩm.

Để đưa image của bạn lên Docker Hub, bạn cần làm theo các bước sau:

1. Đăng nhập vào Docker Hub trên máy tính của bạn:

```
docker login

```

Bạn cần nhập tên đăng nhập và mật khẩu tài khoản Docker Hub của bạn.

1. Đổi tên image của bạn thành định dạng `<tên-tài-khoản-Docker-Hub>/<tên-image>:<tag>` bằng cách sử dụng lệnh:

```
docker tag <tên-image> <tên-tài-khoản-Docker-Hub>/<tên-image>:<tag>

```

Ví dụ:

```
docker tag my-node-app my-dockerhub-account/my-node-app:v1.0.0

```

1. Push image lên Docker Hub bằng lệnh:

```
docker push <tên-tài-khoản-Docker-Hub>/<tên-image>:<tag>

```

Ví dụ:

```
docker push my-dockerhub-account/my-node-app:v1.0.0

```

Sau khi push thành công, image của bạn sẽ được đưa lên Docker Hub và có thể được tải xuống và sử dụng bởi bất kỳ ai có tài khoản Docker Hub.

Sau đó, khi người dùng muốn tải image mới nhất về, họ có thể chạy lệnh:

```
perlCopy code
docker pull my-dockerhub-account/my-node-app

```

Nếu bạn muốn tải về một phiên bản cụ thể, ví dụ **`v1.0.0`**, bạn có thể chạy lệnh:

```
perlCopy code
docker pull my-dockerhub-account/my-node-app:v1.0.0

```