# Tìm Hiểu Quy Trình Vẽ Sequence Diagram

**Sequence Diagram** (Biểu đồ tuần tự) là một công cụ mạnh mẽ trong UML để mô hình hóa quá trình tương tác giữa các đối tượng (objects) trong hệ thống theo trình tự thời gian. Nó giúp hiểu rõ luồng thực thi, sự trao đổi thông điệp (messages), và trách nhiệm của từng thành phần. Quy trình vẽ Sequence Diagram đòi hỏi sự chính xác về logic và thứ tự, đặc biệt hữu ích trong giai đoạn thiết kế và kiểm thử hệ thống.

Trong bài viết này, chúng ta sẽ khám phá chi tiết từng bước xây dựng **Sequence Diagram**, từ việc xác định các thành phần cơ bản đến áp dụng các kỹ thuật nâng cao để mô tả luồng phức tạp.

---

## 1. Các Bước Cơ Bản Trong Quy Trình Vẽ Sequence Diagram

### 1.1 Xác Định Các Đối Tượng Tham Gia (Participants)

Bước đầu tiên là xác định các **đối tượng** (objects) hoặc **thành phần hệ thống** tham gia vào quá trình tương tác. Mỗi đối tượng đại diện cho một thực thể trong hệ thống, chẳng hạn như lớp (class), actor, hoặc hệ thống con.

#### Các bước thực hiện:
- **Liệt kê tất cả các đối tượng** liên quan đến use case cụ thể.
- **Sắp xếp đối tượng theo vai trò**: Đặt actor (người dùng hoặc hệ thống bên ngoài) ở phía trái, các đối tượng nghiệp vụ ở giữa và phải.

#### Ví dụ minh họa:
- **Actor**: Khách hàng.
- **Đối tượng**: `LoginPage`, `AuthenticatioController`, `AuthenticationService`, `AuthenticationRepository`, `Database`.

#### Ký hiệu:
- Đối tượng được biểu diễn bằng **hình chữ nhật** với tên đối tượng và lớp (ví dụ: `user: Customer`).
- **Lifeline** (đường đời): Đường đứt nét dọc dưới mỗi đối tượng, thể hiện vòng đời của đối tượng trong quá trình tương tác.

---

### 1.2 Xác Định Thông Điệp (Messages) và Thứ Tự Thực Thi

Thông điệp là các hành động hoặc lời gọi phương thức giữa các đối tượng. Thứ tự của chúng được sắp xếp từ trên xuống dưới theo dòng thời gian.

#### Các loại thông điệp phổ biến:
1. **Synchronous Message** (Thông điệp đồng bộ): 
   - Được biểu diễn bằng **mũi tên liền nét** kèm đầu mũi tên đặc.
   - Ví dụ: Gọi phương thức `login()` từ `LoginPage` đến `AuthenticationController`.
2. **Asynchronous Message** (Thông điệp bất đồng bộ):
   - Biểu diễn bằng **mũi tên liền nét** với đầu mũi tên rỗng.
   - Ví dụ: Gửi sự kiện `onPaymentComplete` từ hệ thống thanh toán đến `OrderService`.
3. **Return Message** (Phản hồi):
   - Biểu diễn bằng **mũi tên đứt nét**.
   - Ví dụ: `AuthenticationService` trả về kết quả `success: boolean` cho `AuthenticationController`.

#### Các bước thực hiện:
- Liệt kê các thông điệp theo trình tự logic từ khi bắt đầu đến khi kết thúc quy trình.
- Đảm bảo mỗi thông điệp được gán đúng đối tượng gửi và nhận.


#### Ví dụ minh họa:
1. `Khách hàng` → `LoginPage`: Nhập thông tin đăng nhập.
2. `LoginPage` → `AuthenticationController`: Kiểm tra và điều hướng thông tin đến `AuthenticationService`.
3. `AuthenticationService` → `AuthenticationRepository`: Thực hiện logic nghiệp vụ của chức năng **login**, sau đó tiến hành lưu các thông tin cần thiết thông qua việc gọi `AuthenticationRepository`.
4. `AuthenticationRepository` → `Database`: Truy vấn dữ liệu và lưu thông tin cần thiết.

---

### 1.3 Thêm Activation Bars (Thanh Kích Hoạt)

**Activation Bar** (thanh kích hoạt) thể hiện khoảng thời gian một đối tượng đang xử lý một tác vụ. Nó giúp làm rõ thời điểm phương thức được thực thi.

#### Các bước thực hiện:
- Vẽ **hình chữ nhật hẹp** dọc theo lifeline của đối tượng khi nó đang xử lý thông điệp.
- Kéo dài thanh kích hoạt cho đến khi phương thức hoàn tất.

#### Ví dụ:
- Khi `AuthenticationService` xử lý `authenticate()`, một activation bar xuất hiện trên lifeline của nó.

---

## 2. Xử Lý Các Tình Huống Phức Tạp Với Combined Fragments

**Combined Fragments** là các khối logic giúp mô tả các luồng điều kiện, vòng lặp, hoặc luồng song song. Chúng được biểu diễn bằng hình chữ nhật với nhãn và điều kiện.

### 2.1 Fragment Điều Kiện (Alt/Opt)

- **Alt (Alternative)**: Dùng để mô tả các trường hợp "if-else".

   `alt [Điều kiện 1]` => Thông điệp 1

   `else [Điều kiện 2]` => Thông điệp 2

   `end`

- **Opt (Optional)**: Mô tả trường hợp "if" không có else.

   `opt [Điều kiện]` => Thông điệp

   `end`


#### Ví dụ:
- **Alt**: Nếu xác thực thành công, hiển thị trang chủ; ngược lại, hiển thị thông báo lỗi.

---

### 2.2 Fragment Lặp (Loop)

- **Loop** thể hiện một nhóm thông điệp được lặp lại nhiều lần dựa trên điều kiện.

   `loop [5 lần]` => Thông điệp

   `end`


#### Ví dụ:
- Lặp lại việc gửi OTP tối đa 3 lần nếu không nhận được phản hồi.

---


## 3. Kiểm Tra và Tối Ưu Sequence Diagram

Sau khi hoàn thành, cần kiểm tra kỹ lưỡng để đảm bảo tính chính xác:
- **Kiểm tra tính logic**: Thứ tự thông điệp phải đúng với nghiệp vụ thực tế.
- **Kiểm tra phạm vi**: Tránh thêm quá nhiều đối tượng làm biểu đồ phức tạp.
- **Tối ưu hóa**: Nhóm các thông điệp liên quan vào combined fragments.

---

## Tóm Tắt Quy Trình Vẽ Sequence Diagram

#### Các bước thực hiện:
- **Bước 1:** Xác định chức năng cần thiết kế. Bạn dựa vào Use Case Diagram để xác định xem chức năng nào cần thiết kế.
- **Bước 2:** Xác định các bước thực hiện theo nghiệp vụ.
- **Bước 3:** Đối chiếu với Class Diagram để xác định lớp trong hệ thống tham gia vào nghiệp vụ.
- **Bước 4:** Vẽ Sequence Diagarm
- **Bước 5:** Cập nhật lại bản vẽ Class Diagram

Sequence Diagram không chỉ giúp thiết kế hệ thống mà còn là công cụ đắc lực trong việc debug và giao tiếp giữa các bên liên quan. Bằng cách tuân thủ quy trình này, bạn có thể tạo ra các biểu đồ mô tả rõ ràng và hiệu quả luồng nghiệp vụ của hệ thống.