gRPC (gRPC Remote Procedure Calls) là một framework mã nguồn mở do Google phát triển, giúp thực hiện các lời gọi thủ tục từ xa (Remote Procedure Calls - RPC) một cách hiệu quả và tối ưu. Nó được thiết kế để hỗ trợ truyền dữ liệu nhanh chóng giữa các dịch vụ phân tán, đặc biệt là trong mô hình **Microservices**.

---
## Vì sao cần gRPC?
Trong hệ thống **Microservices**, nhiều service phải giao tiếp với nhau để xử lý một request duy nhất. Nếu sử dụng **REST API** với định dạng JSON, mỗi lần truyền dữ liệu, server và client phải **encode và decode** dữ liệu, gây tốn tài nguyên CPU và giảm hiệu suất. gRPC giúp giải quyết vấn đề này bằng cách:
- **Giảm chi phí encode/decode**: Sử dụng **Protocol Buffers (Protobuf)** thay vì JSON giúp giảm kích thước dữ liệu và tăng tốc độ truyền.
- **Hỗ trợ HTTP/2**: gRPC sử dụng HTTP/2 thay vì HTTP/1.1, cho phép **giao tiếp song song** (multiplexing), giảm độ trễ.
- **Streaming dữ liệu**: Hỗ trợ truyền dữ liệu theo **cả hai chiều (bi-directional streaming)**.
- **Định nghĩa API rõ ràng**: gRPC sử dụng file `.proto` để định nghĩa service, giúp việc tạo client/server dễ dàng hơn.

---
## gRPC hoạt động như thế nào?
- **Định nghĩa API bằng ProtoBuf**: Sử dụng file `.proto` để định nghĩa service và message.
- **Generate code tự động**: gRPC compiler sẽ tạo code client/server từ file `.proto` cho nhiều ngôn ngữ như Python, Java, Go, C#, v.v.
- **Giao tiếp giữa client và server**: Client gửi request bằng gRPC protocol, server xử lý và trả về response.
##### Example
```
syntax = "proto3";

service Greeter {
  rpc SayHello (HelloRequest) returns (HelloResponse);
}

message HelloRequest {
  string name = 1;
}

message HelloResponse {
  string message = 1;
}
```

---
## So sánh gRPC và REST API

| **Tiêu chí**       | **gRPC**                         | **REST API**                     |
| ------------------ | -------------------------------- | -------------------------------- |
| Giao thức          | HTTP/2                           | HTTP/1.1                         |
| Định dạng dữ liệu  | Protobuf (nhị phân)              | JSON (text-based)<br>            |
| Tốc độ             | Nhanh hơn (do binary format)     | Chậm hơn (do text-based)<br>     |
| Hỗ trợ Streaming   | Có (bi-directional streaming)    | Không hỗ trợ tốt<br>             |
| Khả năng mở rộng   | Tốt (hỗ trợ nhiều ngôn ngữ)      | Tốt nhưng không tối ưu bằng gRPC |
| Hỗ trợ trình duyệt | Không (chưa hỗ trợ tốt frontend) | Có (qua REST API)<br>            |

---

## Khi nào nên dùng gRPC?
- **Giao tiếp giữa các microservices** trong backend.
- **Hệ thống cần tốc độ cao và truyền dữ liệu hiệu quả**.
- **Streaming dữ liệu** (VD: chat real-time, live video).
- **Hệ thống có nhiều ngôn ngữ lập trình khác nhau** (gRPC hỗ trợ nhiều language bindings).

---
## Tổng kết
- gRPC tối ưu hơn REST API trong môi trường backend-to-backend, nhờ tốc độ cao và sử dụng HTTP/2.
-  Sử dụng Protocol Buffers (Protobuf) giúp giảm kích thước dữ liệu truyền tải.
-  Hỗ trợ streaming và bi-directional communication, phù hợp cho real-time systems.
-  Không phù hợp cho frontend vì chưa hỗ trợ tốt trình duyệt.