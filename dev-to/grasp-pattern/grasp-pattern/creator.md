### 1. Nguyên lý Creator là gì?

- **Nguyên lý Creator** liên quan đến việc gán trách nhiệm tạo một instance của một lớp cho một lớp khác. Điều này giúp giải quyết vấn đề _Lớp nào sẽ chịu trách nhiệm tạo các instance của một đối tượng cụ thể?_

- Nguyên tắc này quy định rằng một lớp nên chịu trách nhiệm tạo đối tượng của một lớp khác nếu một trong các điều kiện sau đây đúng:

  - A chứa đối tượng B.
  - A sử dụng chặt chẽ các đối tượng B.
  - A có dữ liệu khởi tạo sẽ được chuyển cho Đối tượng B.

- **Ví dụ:**
  - Quay lại ví dụ mua hàng ở bài viết [Nguyên Lý Expert Trong GRASP Pattern](https://dev.to/hcmute_project_988df1c63c/nguyen-ly-expert-trong-grasp-pattern-292e). Giả sử một `PurchaseOrder` được tạo thì class nào chịu trách nhiệm để tạo ra các `OrderLine` ?
  - Đáp án chắc chắn phải là `PurchaseOrder`. Vì sao ? Bởi vì một `PurchaseOrder` sẽ chứa các `OrderLine` thì có và chỉ có `PurchaseOrder` có trách nhiệm tạo ra các `OrderLine`.

### 2. Lợi ích của nguyên lý Creator

- **Giảm Coupling giữa các lớp:** Giảm sự phụ thuộc giữa các lớp, tăng tính linh hoạt.
- **Tăng tính rõ ràng và tổ chức trong mã nguồn:** Mã nguồn trực quan, trách nhiệm được phân bổ hợp lý.
- **Hỗ trợ tái sử dụng mã:** Logic tạo đối tượng có thể được tái sử dụng ở nhiều nơi trong hệ thống.
- **Tăng tính bảo trì và dễ mở rộng:** Dễ dàng thay đổi hoặc mở rộng cách khởi tạo đối tượng mà không ảnh hưởng đến các lớp khác.
- **Phù hợp với nguyên lý SRP (Single Responsibility Principle):** Lớp Creator tập trung vào nhiệm vụ tạo đối tượng liên quan, giữ đúng trách nhiệm duy nhất.
- **Dễ dàng kiểm thử (Testing):** Gom logic khởi tạo trong một lớp giúp kiểm thử riêng biệt và hiệu quả hơn.

### 3. Kết luận:

- Nguyên lý Creator là một công cụ mạnh mẽ trong thiết kế phần mềm, giúp phân bổ trách nhiệm khởi tạo đối tượng một cách hợp lý. Việc áp dụng nguyên lý này không chỉ giảm sự phụ thuộc giữa các lớp mà còn tăng tính rõ ràng, tái sử dụng, và bảo trì mã nguồn. Đồng thời, nó hỗ trợ tuân thủ các nguyên lý thiết kế khác như **SRP**, giúp hệ thống trở nên dễ mở rộng và kiểm thử hơn. Đây là một nền tảng quan trọng để xây dựng phần mềm chất lượng cao, dễ quản lý và phát triển lâu dài.
