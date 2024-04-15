# Tối ưu các thứ (noteee)
## I. Về máy tính

### 1. **Tắt Memory integrity**:
#### _B1: Truy cập Window security._
    Win 10: Setting (Win + I) → Update and Security → Window Security.
    Win 11: Setting (Win + I) → Privacy and Security → Window Security.
      
![image](https://github.com/KhangToof/optimize-vm/assets/93634247/d36c1630-e25a-4d3c-b66f-a64f82da5146)
#### _B2: Chọn Device Security → Core isolation details._
    
![image](https://github.com/KhangToof/optimize-vm/assets/93634247/46e5f012-5221-4862-861a-644175b54379)
#### _B3: Tại mục Memory integrity, tắt đi._

![image](https://github.com/KhangToof/optimize-vm/assets/93634247/346537bd-b0e4-4061-8a07-341a39de47b9)

------

### 2. **Tắt Hyper-V**:
#### _B1: Vào Window Search, tìm Turn Windows features on or off._
![image](https://github.com/KhangToof/optimize-vm/assets/93634247/bca76fed-f757-457b-b98e-4b0dd0f62e5a)

#### _B2: Tắt Hyper-V (nếu bạn sử dụng window pro), tiện tay tắt luôn Window HyperVisor platform và Virtual Machine Platform._
![image](https://github.com/KhangToof/optimize-vm/assets/93634247/d438d26b-543d-41c5-98cb-982a1049b240)![image](https://github.com/KhangToof/optimize-vm/assets/93634247/b9ab0f35-c9df-43ac-9cff-1c3f46292d1d)

---
## II. Về VMWare
### 1. **Tắt Accelerate 3D graphics**:
#### _B1: Ở máy ảo Ubuntu master – Ubuntu slave, chuột phải chọn Settings._
![image](https://github.com/KhangToof/optimize-vm/assets/93634247/b93daa8e-b077-4872-af65-6350c5c2d23d)

#### _B2: Chọn vào Display → tắt Accelerate 3D graphics._
![image](https://github.com/KhangToof/optimize-vm/assets/93634247/1d404786-af18-49ac-a56e-570ebdf871fd)

### 2. **Loại bỏ bớt những thứ không cần thiết**:
#### Vẫn ở màn hình Settings trên, ta loại bỏ: CD/DVD, Usb controller, Sound card.
![image](https://github.com/KhangToof/optimize-vm/assets/93634247/6a3ad7ee-758b-49c0-be77-680fafce7676)

### 3. **Điều chỉnh cấu hình**:
#### Điều chỉnh cấu hình cho 2 ubuntu để tối ưu hoạt động.
Máy khoẻ:
  - Ubuntu master: 4GB Memory – 2 processors x 2 cores – 30-40Gb Disk
  - Ubuntu slave: 3GB Memory – 2 processors x 2 cores – 30-40Gb Disk
    
Máy trung bình:
  - Ubuntu master: 3GB Memory – 2 processors x 2 cores – 30-40Gb Disk
  - Ubuntu slave: 1.5-2GB Memory – 2 processors x 1 cores – 30-40Gb Disk
    
Máy yếu:
  - Ubuntu master: 2GB Memory – 2 processors x 1 cores – 20-30Gb Disk
  - Ubuntu slave: 512MB Memory – 1 processors x 1 cores – 10-20Gb Disk

### 4. **Cài đặt cho VMWare High Priority**:
#### _B1: Truy cập Task Manager (Ctrl + Shift + Esc) → Details_.
#### _B2: Tìm đến VMWare.exe → Chuột phải chọn Set Priority → High_.
![image](https://github.com/KhangToof/optimize-vm/assets/93634247/467bd477-8968-4579-b857-863d6d65f4aa)![image](https://github.com/KhangToof/optimize-vm/assets/93634247/5794f78c-f891-4768-a842-63fa5349b03d)

---
## III. Về Ubuntu
### 1. **Tắt cloud-init**:
#### _Ở cả 2 máy ubuntu, ta tiến hành chạy câu lệnh sau (thực hiện ở root)._
    touch /etc/cloud/cloud-init.disabled

### 2. **Điều chỉnh systemd-networkd-wait-online**:
#### _Ở cả 2 máy ubuntu, ta tiến hành chạy câu lệnh sau (thực hiện ở root)._
    sudo systemctl edit --full systemd-networkd-wait-online.service
![image](https://github.com/KhangToof/optimize-vm/assets/93634247/3b277e35-e3a3-470d-b08c-1a6ca06c6b04)
#### Ở chỗ Service ta thêm vào như trên hình (nếu chưa có thì thêm [Service] vào):
    ExecStart=/lib/systemd/systemd-networkd-wait-online –timeout=1
#### Lưu lại

### 3. **Cấp full ổ đĩa đã khai báo cho Ubuntu**:
#### _Ở cả 2 máy ubuntu, ta tiến hành chạy câu lệnh sau (thực hiện ở root)._
    lvextend -l +100%FREE /dev/mapper/ubuntu--vg-ubuntu—lv
    resize2fs /dev/mapper/ubuntu--vg-ubuntu—lv

### 4. **Về vấn đề chạy pig job lâu**:
Theo như mình tìm hiểu thì pig job khi chạy sẽ thường kết nối đến History Server, nhưng ta lại không bật → dẫn đến pig job chạy tương đối lâu!
```
2024-04-06 19:58:11,203 [main] INFO org.apache.hadoop.mapred.ClientServiceDelegate - Application state is completed. FinalApplicationStatus=SUCCEEDED. 
**Redirecting to job history server** 
2024-04-06 19:59:13,112 [main] INFO  org.apache.hadoop.ipc.Client - Retrying connect to server: 0.0.0.0/0.0.0.0:10020. Already tried 0 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
…
```
Để khắc phục thì cơ bản ta chỉ cần chạy thêm historyserver trước khi chạy pig:
    mr-jobhistory-daemon.sh start historyserver

Mình mong là những gì mình tổng hợp trên phần nào giúp việc tối ưu cho công việc học tập  BigDataAnalysis được thuận lợi hơn 🐻🐻
