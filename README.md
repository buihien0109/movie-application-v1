## Trang web xem phim trực tuyến

Link demo: http://103.237.147.34:8888/

### Triển khai ứng dụng

Sau khi clone source về máy, có thể triển khai ứng dụng theo 2 cách:

#### 1. Chạy ứng dụng với maven

```bash
mvn spring-boot:run
```

#### 2. Triển khai ứng dụng với Docker Compose

```
docker-compose up -d
```

### Công nghệ sử dụng
- Spring Boot
- Spring Security
- Spring Data JPA
- Thymeleaf
- MySQL
- Docker
- Docker Compose
- ...

### Sơ đồ thiết kế cơ sở dữ liệu

- https://dbdiagram.io/d/db-movie-app-659cc597ac844320ae80c2f9

### Các chức năng chính

#### 1. Người dùng
- Tìm kiếm phim theo danh mục, thể loại, quốc gia
- Xem thông tin chi tiết phim
- Xem phim
- Xem thông tin các bài viết
- Đăng ký tài khoản, đăng nhập, đăng xuất
- Quản lý thông tin cá nhân
- Review phim, thêm phim vào danh sách yêu thích, xem lịch sử xem phim, quản lý đơn hàng, ...
- Tìm kiếm, xem, mua phim trả phí

#### 2. Quản trị viên

Trang đăng nhập : /dang-nhap

```
Role : ROLE_ADMIN
Username : admin@gmail.com
Password : 123

Role : ROLE_USER
Username : user@gmail.com
Password : 123
```

- Xem các thông số thống kê tổng quan
- Quản lý phim
- Quản lý thể loại
- Quản lý tin tức
- Quản lý người dùng
- Quản lý diễn viên
- Quản lý đạo diễn
- Quản lý đơn hàng
- ...

### Github Action

```yaml
name: Java CI/CD Pipeline

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2

    - name: Set up JDK 17
      uses: actions/setup-java@v2
      with:
        java-version: '17'
        distribution: 'temurin'

    - name: Build with Maven
      working-directory: ./movie-app
      run: |
        echo "Maven version:"
        mvn -version
        mvn -B clean install

    - name: Build Docker Image
      working-directory: ./movie-app
      run: docker build -t buihien0109/movie-app:latest .

    - name: Login to Docker Hub
      run: echo ${{ secrets.DOCKER_PASSWORD }} | docker login -u ${{ secrets.DOCKER_USERNAME }} --password-stdin

    - name: Push Docker Image to Docker Hub
      run: docker push buihien0109/movie-app:latest
```