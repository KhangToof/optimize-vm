# Tối ưu các thứ (noteee)
### I. Về máy tính
1. **Tắt Memory integrity**:
  - B1: Truy cập Window security
    - Win 10: Setting (Win + I) → Update and Security → Window Security
    - Win 11: Setting (Win + I) → Privacy and Security → Window Security
![image](https://github.com/KhangToof/optimize-vm/assets/93634247/d36c1630-e25a-4d3c-b66f-a64f82da5146)
  - B2: Chọn Device Security → Core isolation details
![image](https://github.com/KhangToof/optimize-vm/assets/93634247/46e5f012-5221-4862-861a-644175b54379)
  - B3: Tại mục Memory integrity, tắt đi
![image](https://github.com/KhangToof/optimize-vm/assets/93634247/346537bd-b0e4-4061-8a07-341a39de47b9)


2. **Tắt Hyper-V**:
   - Mở Control Panel -> Programs -> Turn Windows features on or off.
   - Bỏ chọn Hyper-V để tắt tính năng ảo hóa này, giúp cải thiện hiệu suất cho các ứng dụng khác.
---
### II. Về VMWare
1. **Tắt Accelerate 3D graphics**:
   - Trong VMWare, vào Edit Virtual Machine Settings của máy ảo.
   - Tắt tính năng Accelerate 3D graphics nếu không sử dụng để giảm tải cho máy ảo.

2. **Loại bỏ bớt những thứ không cần thiết**:
   - Xác định và gỡ bỏ các ứng dụng, dịch vụ không cần thiết để giảm tải cho máy ảo.

3. **Điều chỉnh cấu hình**:
   - Đảm bảo cấu hình CPU, RAM, và dung lượng ổ đĩa đủ cho yêu cầu công việc mà không quá tải.

4. **Cài đặt cho VMWare High Priority**:
   - Thiết lập ưu tiên cao cho quá trình VMWare trong Task Manager để đảm bảo ưu tiên xử lý cho máy ảo.
---
### III. Về Ubuntu
1. **Tắt cloud-init**:
   - Sửa file `/etc/cloud/cloud.cfg` và đặt `disable_cloud_init: true` để tắt tính năng cloud-init.

2. **Điều chỉnh systemd-networkd-wait-online**:
   - Chỉnh sửa file `/etc/systemd/system/network-online.target.wants/systemd-networkd-wait-online.service` và thêm tham số `TimeoutStartSec=1`.

3. **Cấp full ổ đĩa đã khai báo cho Ubuntu**:
   - Đảm bảo cấp đủ dung lượng ổ đĩa cho Ubuntu để tránh tình trạng quá tải khi chạy Hadoop.

4. **Về vấn đề chạy pig job lâu**:
   - Xác định và giải quyết các vấn đề về tài nguyên, cấu hình, hoặc mã nguồn trong Pig job để cải thiện thời gian chạy.

---
