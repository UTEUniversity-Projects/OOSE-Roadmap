# Agile Development Techniques

Trong phần này, chúng ta sẽ thảo luận về các kỹ thuật phát triển phần mềm theo phương pháp **Agile**, trong đó tập trung vào **Extreme Programming (XP)** - một trong những phương pháp Agile nổi bật được giới thiệu bởi **Kent Beck** vào những năm 1990.

## 📌 Giới thiệu về Extreme Programming

Trong **Extreme Programming (XP)**, các yêu cầu được biểu diễn dưới dạng **user stories** và triển khai qua một loạt các nhiệm vụ. Các lập trình viên làm việc theo cặp và viết kiểm thử cho từng nhiệm vụ trước khi lập trình, đồng thời đảm bảo tất cả kiểm thử chạy thành công khi tích hợp mã. Hệ thống được phát hành trong khoảng thời gian ngắn.

## 🔥 User Stories là gì?

**User stories** là cách mô tả yêu cầu bằng các kịch bản sử dụng thực tế. Thay vì tài liệu yêu cầu truyền thống, khách hàng làm việc trực tiếp với nhóm phát triển để xác định các tình huống sử dụng cụ thể.

## 🚀 Các kỹ thuật phát triển:

#### 1️⃣ Refactoring

Thay vì tài liệu yêu cầu truyền thống, khách hàng làm việc trực tiếp với nhóm phát triển để xác định các tình huống sử dụng cụ thể. Khi lập trình viên phát hiện điểm có thể tối ưu, họ thực hiện ngay cả khi chưa có yêu cầu cấp bách.
🔥 **Ưu điểm:**

- Duy trì cấu trúc phần mềm.
- Hạn chế code trùng lặp.
- Cải thiện khả năng bảo trì.
- Đảm bảo hệ thống dễ hiểu và dễ thay đổi khi cần.

### 2️⃣ Test-First Development

Thay vì viết mã trước rồi kiểm thử sau, **Test-First Development** trong **Extreme Programming (XP)** yêu cầu viết kiểm thử **trước** khi triển khai tính năng. Điều này giúp phát hiện lỗi sớm và đảm bảo mã đúng với yêu cầu.

🔹 **Đặc điểm chính của kiểm thử trong XP:**

- Viết kiểm thử trước khi lập trình.
- Phát triển kiểm thử dần từ các kịch bản người dùng.
- Khách hàng tham gia vào quá trình kiểm thử và xác nhận.
- Sử dụng khung kiểm thử tự động (như **JUnit**).

Cách tiếp cận này giúp xác định rõ yêu cầu, tránh hiểu sai giao diện và chức năng. Ngoài ra, **kiểm thử tự động** đảm bảo mọi thay đổi không phá vỡ hệ thống. Tuy nhiên, việc đảm bảo đầy đủ phạm vi kiểm thử vẫn là một thách thức quan trọng.

### 2️⃣ Pair Programming

**Pair Programming** là một kỹ thuật trong **(XP)**, _trong đó hai lập trình viên cùng ngồi trên một máy tính_ để phát triển phần mềm. Tuy nhiên, các cặp không cố định mà thay đổi linh hoạt, giúp tất cả thành viên làm việc cùng nhau trong quá trình phát triển.

🔥 **Lợi ích:**

- **Tăng tính sở hữu tập thể** – Mã nguồn thuộc về cả nhóm, không phải cá nhân. Điều này giúp mọi người cùng chịu trách nhiệm về chất lượng phần mềm.
- **Kiểm tra mã nguồn liên tục** – Mỗi dòng mã đều được xem xét bởi ít nhất hai người, giúp giảm lỗi nhanh hơn so với quy trình kiểm tra chính thức.
- **Thúc đẩy tái cấu trúc mã (Refactoring)** – Khi có người thứ hai cùng tham gia, việc cải tiến mã nguồn được hỗ trợ và dễ dàng hơn.

⚡**Hiệu suất:**

Mặc dù có thể khiến tốc độ viết mã giảm, nhưng nghiên cứu cho thấy:

- **Lập trình viên làm việc theo cặp ít mắc lỗi hơn** và cần ít thời gian sửa lỗi sau này.
- **Đối với lập trình viên có kinh nghiệm, năng suất có thể giảm** so với làm việc độc lập.
- Tuy nhiên, **việc chia sẻ kiến thức trong nhóm giúp giảm rủi ro** khi có thành viên rời dự án.

# 📌 Kết luận:

XP đã mang đến nhiều thực tiễn quan trọng, giúp nâng cao chất lượng phần mềm và tăng cường khả năng thích ứng với thay đổi. Nhiều kỹ thuật như Test-Driven Development (TDD), Pair Programming, và Continuous Integration không chỉ được áp dụng trong XP mà còn trở thành tiêu chuẩn phổ biến trong ngành công nghiệp phần mềm hiện nay.
