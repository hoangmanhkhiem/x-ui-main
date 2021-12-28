# x-ui
Hỗ trợ bảng điều khiển xray đa giao thức và nhiều người dùng

# Đặc trưng
- Giám sát tình trạng hệ thống
-Hỗ trợ đa người dùng và đa giao thức, hoạt động trực quan hóa trang web
-Giao thức được hỗ trợ: vmess, vless, trojan, shadowsocks, dokodemo-door, tất, http
-Hỗ trợ cấu hình nhiều cấu hình truyền hơn
- Thống kê lưu lượng, giới hạn lưu lượng, giới hạn thời gian hết hạn
-Mẫu cấu hình xray có thể tùy chỉnh
-Hỗ trợ bảng điều khiển truy cập https (mang theo tên miền + chứng chỉ ssl của riêng bạn)
-Các mục cấu hình nâng cao hơn, xem bảng điều khiển để biết chi tiết

# Cài đặt & Nâng cấp
```
bash <(curl -Ls https://raw.githubusercontent.com/hoangmanhkhiem/x-ui/master/install.sh)
```

## Cài đặt và nâng cấp thủ công
1. Đầu tiên tải xuống gói nén mới nhất từ ​​https://github.com/hoangmanhkhiem/x-ui/releases, thường chọn kiến ​​trúc `amd64`
2. Sau đó tải gói nén lên thư mục `/ root /` của máy chủ và sử dụng người dùng `root` để đăng nhập vào máy chủ

> Nếu kiến ​​trúc cpu máy chủ của bạn không phải là `amd64`, hãy thay thế` amd64` trong lệnh bằng một kiến ​​trúc khác

```
cd /root/
rm x-ui/ /usr/local/x-ui/ /usr/bin/x-ui -rf
tar zxvf x-ui-linux-amd64.tar.gz
chmod +x x-ui/x-ui x-ui/bin/xray-linux-* x-ui/x-ui.sh
cp x-ui/x-ui.sh /usr/bin/x-ui
cp -f x-ui/x-ui.service /etc/systemd/system/
mv x-ui/ /usr/local/
systemctl daemon-reload
systemctl enable x-ui
systemctl restart x-ui
```

## Cài đặt bằng docker

> Hướng dẫn về docker và hình ảnh về docker này được tạo bởi[Chasing66](https://github.com/Chasing66)

1. Cài đặt docker
```shell
curl -fsSL https://get.docker.com | sh
```
2. Cài đặt x-ui
```shell
mkdir x-ui && cd x-ui
docker run -itd --network=host \
    -v $PWD/db/:/etc/x-ui/ \
    -v $PWD/cert/:/root/cert/ \
    --name x-ui --restart=unless-stopped \
    enwaiax/x-ui:latest
```
> Xây dựng hình ảnh của riêng bạn
```shell
docker build -t x-ui .
```
## Hệ thống đề xuất
-CentOS 7+
-Ubuntu 16+
-Debian 8+

# vấn đề thường gặp

## Di chuyển từ v2-ui
Trước tiên hãy cài đặt phiên bản mới nhất của x-ui trên máy chủ nơi v2-ui được cài đặt, sau đó sử dụng lệnh sau để di chuyển, lệnh này sẽ di chuyển `tất cả dữ liệu tài khoản gửi đến 'của v2-ui của máy sang x-ui,' cài đặt bảng điều khiển và tên người dùng và mật khẩu Sẽ không di chuyển`
> Sau khi di chuyển thành công, vui lòng `đóng v2-ui` và` khởi động lại x-ui`, nếu không quá trình chuyển đến của v2-ui và đầu vào của x-ui sẽ gây ra `xung đột cổng '
``
x-ui v2-ui
``

## vấn đề đóng lại
Tất cả các loại vấn đề của x-ui đều ổn
