TCS34725 Raspberry Pi 3 B+ Driver & User Space IOCTL Tester
THANH VIEN:
Lê Hà Tuấn Cảnh_22146273
Nguyễn Chí Kiên_22146336
Nguyễn Văn Hoàng_22146310
============================================================
Ứng dung thực tế 
Nhận dạng màu sắc trong các hệ thống phân loại sản phẩm.
Robot tránh vạch hoặc nhận dạng vạch màu.
Điều chỉnh ánh sáng thông minh dựa trên màu sắc môi trường.
Cảm biến môi trường trong các thiết bị IoT.
============================================================
Author: CDT  
License: GPL  
Target: Raspberry Pi 3 B+  
Sensor: TCS34725 
-------------------------
Directory Structure:
-------------------------
driver_tcs34725/
├── tcs34725_driver.c       
├── test_tcs.c  
├── ioctl.c       
├── Makefile               
└── ReadMe.txt     
================================================================
Cách cài đặt TCS34725
Yêu cầu phần cứng:
Cảm biến TCS34725
Raspberry Pi 3 B+
Dây nối
================================================================
Kết nối chân (sử dụng bộ I2C1)
TCS34725	Raspberry Pi 3 B+
VIN	        Pin 1
GND	        Pin 6
SDA	        Pin 11
SCL	        Pin 5
================================================================
Cấu hình module
Bước 1: 
------------------
cd /boot/firmware
(raspberry pi 3)
-----------------
cd /boot
-----------------
Bước 2:
Tìm đến file có đầu là bcm2710 và đuôi là .dtb

Bước 3:
Chuyển đổi file bạn vừa kiểm ở trên từ .dtb sang .dts
------------------------------------------------------------------------
sudo dtc -I dtb -O dts -o bcm2712-rpi-3-plus.dts bcm2712-rpi-3-plus.dtb
------------------------------------------------------------------------
Bước 4:
Truy cập vào file .dts vừa tạo.
----------------------------------
sudo nano bcm2712-rpi-3-plus.dts
----------------------------------
Bước 5:
Tìm đến: i2c@7e205000
và nhập vào đoạn sau:
tcs34725@29{ 
    compatible = "key,tcs34725"; 
    reg = <0x29>; 
};
Bước 6:
Chuyển đổi file bạn vừa kiểm ở trên từ .dts sang .dtb
------------------------------------------------------------------
sudo dtc -I dts -O dtb -o bcm2712-rpi-3-plus.dtb bcm2712-rpi-3-plus.dts
------------------------------------------------------------------
Cài đặt
Truy cập vào folder lưu các file driver.
-------
make
-------
Sau đó:
-----------------------------------
sudo insmod TCS34725_driver.ko
-----------------------------------
Kiểm tra log kernel và chạy
Kiểm tra:
----------------
dmesg | tail
----------------
Sau đó chạy:
---------------------------
gcc test_tcs.c -o run
sudo ./run
---------------------------
Gỡ cài đặt và dọn dẹp file
---------------------------
sudo rmmod tcs34725_driver
make clean
-----------------------------------------------------------
