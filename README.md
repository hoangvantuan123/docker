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

Để tích hợp cả hai thư mục client và server vào Docker, bạn có thể tạo hai container Docker riêng biệt cho mỗi thư mục và sử dụng Docker Compose để quản lý chúng. Với cách tiếp cận này, bạn có thể chạy các câu lệnh `npm run` khác nhau cho từng container.

Dưới đây là một ví dụ cấu trúc thư mục và tệp tin `Dockerfile` cho mỗi container:

1. Thư mục `client`:
```
client/
  |- Dockerfile
  |- package.json
  |- src/
  |- ...

```
File Dockerfile:
```Dockerfile
FROM node:latest

WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .

EXPOSE 3000

CMD [ "npm", "run", "start" ]
```

2. Thư mục `server`:
```
server/
  |- Dockerfile
  |- package.json
  |- index.js
  |- ...

```
File Dockerfile:
```Dockerfile
FROM node:latest

WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .

EXPOSE 8080

CMD [ "npm", "run", "start" ]
```

Sau đó, bạn có thể tạo một tệp tin `docker-compose.yml` để quản lý cả hai container, như sau:

```yaml
version: '3.8'

services:
  client:
    build:
      context: ./client
      dockerfile: Dockerfile
    ports:
      - "3000:3000"
    volumes:
      - ./client:/app
  server:
    build:
      context: ./server
      dockerfile: Dockerfile
    ports:
      - "8080:8080"
    volumes:
      - ./server:/app
```

Trong file `docker-compose.yml`, các dịch vụ `client` và `server` được định nghĩa bằng cách sử dụng các thông số build, cổng và thư mục lưu trữ để quản lý các container tương ứng. Bạn có thể chạy lệnh `docker-compose up` để chạy cả hai container cùng lúc.

Sau khi chạy lệnh này, Docker sẽ tạo và khởi chạy các container dựa trên cấu hình được định nghĩa trong file `docker-compose.yml`. Bạn có thể truy cập ứng dụng của mình trên các cổng tương ứng, ví dụ `localhost:3000` cho container `client` và `localhost:8080` cho container `server`.

Sau đó, để build các ứng dụng này, bạn có thể sử dụng lệnh sau:

```yaml
docker build -t client-image -f client/Dockerfile .
docker build -t server-image -f server/Dockerfile .
```
Trong đó:

-t để chỉ định tên và tag cho image (ví dụ: client-image và server-image)
-f để chỉ định đường dẫn đến Dockerfile cho mỗi ứng dụng (ví dụ: client/Dockerfile và server/Dockerfile)
. để chỉ định đường dẫn đến thư mục chứa Dockerfile (ví dụ: dấu chấm để chỉ định rằng Dockerfile được đặt trong thư mục hiện tại)

Sau đó, bạn có thể sử dụng lệnh sau để khởi chạy cả hai ứng dụng:

Copy code
docker-compose up
Lệnh này sẽ tự động tạo và chạy các container cho cả hai ứng dụng. Các container này sẽ được kết nối với nhau thông qua mạng mặc định của Docker Compose.

Nếu bạn muốn tắt các container, bạn có thể sử dụng tổ hợp phím Ctrl + C hoặc sử dụng lệnh:

Copy code
docker-compose down
Lệnh này sẽ dừng và xóa các container đã được tạo ra bởi Docker Compose.
----------------------------------------------------------------
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