# 🚀 Hướng Dẫn Cài Đặt GitHub, Docker và Build Superset

<div align="center">
  <img src="https://github.githubassets.com/images/modules/logos_page/GitHub-Logo.png" width="200" alt="GitHub Logo"/>
  <img src="https://www.docker.com/sites/default/files/d8/2019-07/horizontal-logo-monochromatic-white.png" width="200" alt="Docker Logo"/>
</div>

## 📑 Mục Lục
- [Cài đặt GitHub](#cài-đặt-github)
- [Cài đặt Docker](#cài-đặt-docker)
- [Build Superset](#build-superset)

## 📑 Cấu hình máy chủ
=====================
Phần mềm được cài đặt trên máy chủ nên có:
- Hệ điều hành: Ubuntu 22.04 Server
- CPU: 4 core (Tối thiểu 2 core, khuyến nghị 4 core trở lên)
- RAM: 8GB (Tối thiểu 4GB, khuyến nghị 8GB trở lên)
- Bộ nhớ: 100GB (Tối thiểu 50GB, khuyến nghị 100GB trở lên)
- Docker & Docker Compose: Đã được cài đặt
- Cho phép truy cập SSH từ xa


## 🔰 Cài đặt GitHub

### 1. Cập nhật hệ thống

```bash
sudo apt update && sudo apt upgrade -y
```

### 2. Cài đặt Git

```bash
sudo apt install git -y
```


### 3. Kiểm tra phiên bản Git

```bash
git --version
```
Ví dụ:
```bash
git version 2.41.0
```

### 4. Cấu hình Git(tùy chọn)
Nếu muốn sử dụng Git trên hệ thống, bạn có thể cấu hình Git theo các bước sau:

```bash
git config --global user.name "Tên Người Dùng"
git config --global user.email "Email"
```
Kiểm tra cấu hình Git:
```bash
git config --list
```

## 🔰 Cài đặt Docker

### 1. Cập nhật hệ thống

```bash
sudo apt update && sudo apt upgrade -y
```

### 2. Thêm khóa GPG của Docker

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

### 3. Thêm repository Docker vào danh sách nguồn của APT

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### 4. Kiểm tra thông tin gói Docker

```bash
sudo apt-cache policy docker-ce
```

### 5. Cài đặt Docker 

```bash
sudo apt install docker-ce -y
```

### 6. Kiểm tra phiên bản Docker

```bash
docker --version
```
Ví dụ:
```bash
docker version 24.0.5
```

### 7. Kiểm tra trạng thái Docker

```bash
sudo systemctl status docker
```

### 8. Khởi động lại Docker

```bash
sudo systemctl start docker
```

## 🔰 Build Superset

### 1. Clone repository Superset

```bash
git clone --depth=1 https://github.com/apache/superset.git
```

### 2. Khởi chạy Superset thông qua Docker Compose

#Option 1: for an interactive development environment
```bash
cd superset
# The --build argument insures all the layers are up-to-date
docker compose up --build
```

#Option 2: build a set of immutable images from the local branch
```bash
cd superset
docker compose -f docker-compose-non-dev.yml up
```

#Option 3: boot up an official release
```bash
cd superset
export TAG=3.1.1
docker compose -f docker-compose-image-tag.yml up
```





