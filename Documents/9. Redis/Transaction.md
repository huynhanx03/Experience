## Các lệnh chính trong Redis Transaction**

| **Lệnh**  | **Mô tả**                                                                                      |
| --------- | ---------------------------------------------------------------------------------------------- |
| MULTI     | Bắt đầu một transaction. Redis sẽ đưa tất cả các lệnh tiếp theo vào hàng đợi.                  |
| EXEC      | Thực thi tất cả các lệnh đã xếp hàng từ MULTI.                                                 |
| DISCARD   | Hủy bỏ transaction và xóa hàng đợi lệnh.                                                       |
| WATCH key | Giám sát một hoặc nhiều key trước khi thực hiện transaction, hỗ trợ cơ chế optimistic locking. |
| UNWATCH   | Hủy giám sát các key đã WATCH.                                                                 |

##### Example
###### 1. Transaction cơ bản
```
MULTI
SET user:1 "Nhân"
SET age:1 22
INCR balance:1
EXEC
```
**Giải thích**:
- `MULTI` bắt đầu transaction.
- Các lệnh `SET` và `INCR` được xếp hàng.
- `EXEC` thực thi tất cả lệnh một cách nguyên tử.

###### 2. Hủy transaction
```
MULTI
SET user:2 "Mai"
SET age:2 23
DISCARD
```
`DISCARD` hủy bỏ transaction, các lệnh trước đó không được thực hiện.

###### 3. Sử dụng `WATCH` (Optimistic Locking)
```
WATCH balance:1    
MULTI
INCR balance:1
EXEC               
```
**Giải thích**:
- `WATCH balance:1` giám sát khóa này.
- Nếu có tiến trình khác thay đổi `balance:1` trước khi `EXEC`, thì transaction sẽ bị hủy.

---
## ACID của Transaction trong Redis
- **Atomicity (Tính nguyên tử)**: Có, tất cả lệnh trong `MULTI ... EXEC` được thực hiện hoặc không có lệnh nào được thực hiện.
- **Consistency (Tính nhất quán)**: Phụ thuộc vào ứng dụng, Redis không có ràng buộc chặt chẽ như SQL.
- **Isolation (Tính cô lập)**: Có, trong transaction, các lệnh không bị gián đoạn bởi tiến trình khác.
- **Durability (Tính bền vững)**: Không, nếu Redis bị crash, dữ liệu có thể không được lưu nếu không bật **AOF (Append-Only File)**.

---
## Khi nào nên dùng Redis Transaction?
- Khi cần thực hiện nhiều lệnh một cách nguyên tử (atomic).  
- Khi muốn tránh race condition bằng `WATCH`.  
- Không nên dùng nếu cần rollback khi gặp lỗi, vì Redis không hỗ trợ rollback.

**Tóm lại:** Redis transaction mạnh mẽ nhưng không có rollback, vì vậy cần thiết kế logic phù hợp với ứng dụng.