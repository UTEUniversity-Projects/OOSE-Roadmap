### Nguyên lý Creator là gì?

- **Nguyên lý Creator** liên quan đến việc gán trách nhiệm tạo một instance của một lớp cho một lớp khác. Điều này giúp giải quyết vấn đề _Đối tượng này được tạo ra từ đâu?_

- Nguyên tắc này quy định rằng một lớp nên chịu trách nhiệm tạo đối tượng của một lớp khác nếu một trong các điều kiện sau đây đúng: lớp đó chứa đối tượng cần tạo, lớp đó dùng nhiều đối tượng cần tạo, hoặc lớp đó có dữ liệu cần thiết để khởi tạo đối tượng.

- **Ví dụ:**
  - Trong hệ thống bán hàng, lớp `Sale` nên chịu trách nhiệm tạo đối tượng `SalesLineItem` vì Sale chứa các đối tượng `SalesLineItem`. Phương thức `makeLineItem(quantity)` sẽ được thêm vào lớp Sale để tạo các đối tượng `SalesLineItem`.
  - Lớp `Diary` chứa một list các `Note`, vì vậy class `Diary` có thể chịu tráchnhiệm trong việc tạo ra các đối tượng Note mới bởi vì class `Diary` đã có sẵn những thông tin về `Note`, đảm bảo một đối tượng mới có thể được tạo ra và thêm vào.

### Lợi ích

- **Ứng dụng:**
  - Hướng dẫn trong việc gán trách nhiệm tạo đối tượng.
  - Giúp tìm ra lớp nào chịu trách nhiệm tạo đối tượng.
- **Ưu điểm:**
  - Nguyễn lý Creator hỗ trợ giảm coupling giữa các lớp.
  - Ít phụ thuộc hơn và tính tái sử dụng cao hơn.
  - Coupling không tăng lên vì lớp được tạo ra hiển thị với lớp Creator.

### Kết luận:

- Nguyên lý Creator cung cấp một phương pháp hiệu quả để xác định và gán trách nhiệm tạo đối tượng trong thiết kế hướng đối tượng. Nó giúp duy trì coupling thấp và tối ưu hóa sự tái sử dụng của các lớp bằng cách xác định rõ ràng mối quan hệ và trách nhiệm của các lớp trong việc tạo ra đối tượng.
