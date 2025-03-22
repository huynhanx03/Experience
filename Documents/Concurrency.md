
Concurrency (Đồng thời) tức là nhiều phép tính toán cùng xảy ra tại cùng một thời điểm. Ví dụ:
```
- Nhiều máy tính trong một mạng máy tính
- Nhiều ứng dụng cùng chạy trong một máy tính
- Nhiều bộ xử lý (processor) trong một máy tính (nhiều nhân trong một chip)
- Một website cần xử lý nhiều lượng truy cập cùng lúc
```

---
## Hai mô hình phổ biến

- Shared Memory: các concurrent mô-đun tương tác với nhau thông qua việc đọc và ghi các shared objects trong bộ nhớ.
```
A và B chia sẻ chung các objects màu cam, trong khi các objects màu xanh là private.
```

- Message Passing: các concurrent mô-đun tương tác với nhau bằng cách gửi các message tới bên kia thông qua một kênh giao tiếp.
```
A và B là 2 máy tính ở trong cùng một mạng, giao tiếp thông qua kết nối mạng.
```

---
## Process vs Thread

|                   | Process                                                             | Thread                                                                 |
| ----------------- | ------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| Khái niệm         | Là một chương trình đang thực thi (đang chạy)                       | Là một thành phần con của process, có thể chạy đồng thời nhiều thread. |
| Bộ nhớ            | Các process là độc lập, không chia sẻ không gian nhớ với nhau       | Các threads chia sẻ không gian nhớ<br>                                 |
| Khởi tạo          | Cần nhiều system call để tạo nhiều process, tốn nhiều thời gian hơn | Có thể tạo nhiều threads với một system call, tốn ít thời gian hơn<br> |
| Chấm dứt          | Tốn thời gian hơn so với thread                                     | Tốn ít thời gian hơn so với process<br>                                |
| Giao tiếp         | Cần sử dụng IPC, tốn kém hơn                                        | Ít tốn kém hơn so với process<br>                                      |
| Context Switching | Chậm hơn threads                                                    | Nhanh hơn nhiều so với process                                         |

---
## Trạng thái của process

- **Running:** Tiến trình đang được thực thi trên bộ vi xử lý và đang thực hiện các lệnh.
- **Ready:** Tiến trình sẵn sàng thực thi, nhưng hệ điều hành (OS) chưa quyết định chạy nó vào thời điểm này.
- **Blocked:** Tiến trình đã hoàn thành một hành động nào đó ngăn cản nó chạy cho đến khi một sự kiện khác xảy ra. Ví dụ, nếu tiến trình yêu cầu nhập/xuất (I/O) vào đĩa, nó sẽ bị chặn. Điều này sẽ cho phép tiến trình khác sử dụng CPU.