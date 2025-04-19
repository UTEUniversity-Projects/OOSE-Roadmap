# Kiến Trúc Hệ Thống Lớn và Phức Tạp

## 📘 Tổng Quan

Trong các chương trước, chúng ta chủ yếu đề cập đến các hệ thống nhỏ với quy mô vài lập trình viên và vòng lặp kéo dài vài tháng. Tuy nhiên, với hệ thống lớn và phức tạp hơn, ta phải đối mặt với nhiều vấn đề hơn như: khả năng mở rộng, quản lý đội ngũ lớn, phân vùng trách nhiệm và giữ vững chất lượng sản phẩm.

Câu hỏi đặt ra là: **Liệu UML có đủ khả năng để hỗ trợ phát triển các hệ thống lớn trong mô hình Lặp và Gia tăng (Iterative and Incremental Framework)?**  
Câu trả lời là có — nếu biết sử dụng **Package Diagram**, kiến trúc theo hướng **Architecture-Centric**, và các mẫu thiết kế như **Facade**.

---

## 📦 UML Package Diagram – Công Cụ Quản Lý Quy Mô

### ✅ UML Package Là Gì?

**Package** là một vùng chứa logic giúp nhóm các phần tử UML có liên quan với nhau — giống như thư mục chứa file trong hệ điều hành. Package giúp:

- Nhóm các lớp hoặc Use Case liên quan thành **subsystems**.
- Cho phép các nhóm làm việc **song song và độc lập**.
- Tránh **trùng tên** giữa các nhóm làm việc.

> Ví dụ: Package `GUI` chứa các lớp liên quan đến giao diện người dùng.

### ✅ Sơ Đồ Package

- Trình bày **mối quan hệ phụ thuộc** giữa các package.
- Cung cấp góc nhìn **cấp cao (high-level)**, không đi sâu vào chi tiết từng phần tử.
- Có thể lồng các package vào nhau như hệ thống thư mục.

> Ví dụ: mô hình ba lớp (Three-tier model) với `Presentation` phụ thuộc `Business`.

---

## 🔄 Giao Tiếp Giữa Các Package – Facade Pattern

### ❌ Vấn Đề:

Nếu các lớp trong `Subsystem A` gọi trực tiếp các lớp trong `Subsystem B`, khi thay thế một subsystem sẽ rất khó theo dõi và kiểm soát.

> Ví dụ: muốn thay `Subsystem A` (UI terminal) bằng giao diện mới, ta cần thay toàn bộ các lớp tương ứng. Rất phức tạp.

### ✅ Giải Pháp: **Facade**

- Tạo ra một **lớp trung gian** duy nhất trong mỗi subsystem — gọi là **Facade**.
- Tất cả các tương tác với subsystem đều phải **thông qua Facade**, không gọi trực tiếp vào bên trong.
- Khi cần thay đổi hệ thống bên trong, chỉ cần điều chỉnh Facade.

### ✅ Ưu Điểm:

- Đơn giản hóa việc bảo trì.
- Hạn chế phụ thuộc chéo.
- Cải thiện khả năng làm việc **độc lập giữa các nhóm**.

> Java hỗ trợ rất tốt với mức **package visibility**: các lớp `package-private` chỉ có thể truy cập trong cùng package. Nếu chỉ để `Facade` là `public`, các lớp khác sẽ bị ẩn khỏi bên ngoài.

---

## 🏛️ Phát Triển Theo Hướng Kiến Trúc (Architecture-Centric Development)

### ✅ Khái Niệm

**Rational Unified Process** nhấn mạnh phát triển theo kiến trúc (Architecture-Centric).  
Hệ thống cần được chia thành **các subsystem nhỏ**, được lên kế hoạch từ sớm và duy trì bởi **một nhóm kiến trúc trung tâm**.

### 🎯 Vai Trò Của Nhóm Kiến Trúc

- Sở hữu và bảo trì sơ đồ package cấp cao.
- Quản lý tất cả các **interface giữa các subsystem** (các Facade).
- Đảm bảo rằng mọi thay đổi với các interface đều được kiểm soát.

> Điều này giúp kiểm soát tác động thay đổi, tránh phá vỡ cấu trúc tổng thể.

---

## 📋 Ví Dụ: Hệ Thống Command & Control

Nhóm kiến trúc xác định các khối chức năng chính và phân chia thành sơ đồ package:

1. **Tracking Subsystem**
2. **Display Subsystem**
3. **Weapons Subsystem**
4. **Communication Subsystem**

> Mỗi subsystem được xây dựng như một hệ thống độc lập, có sơ đồ Use Case riêng và có thể phát triển song song.

---

## 🧩 Xử Lý Use Case Lớn

### ❌ Vấn Đề:

Một số Use Case được xác định trong giai đoạn Elaboration có thể **quá lớn** để hoàn thành trong một vòng lặp.

### ✅ Giải Pháp:

- **Không kéo dài vòng lặp** (vì sẽ tăng độ phức tạp).
- **Chia nhỏ Use Case** thành các **phiên bản dễ quản lý**, mỗi phiên bản được hoàn thành trong một iteration.

> Ví dụ: Use Case “Fire Torpedoes”
- **Version 1**: Mở nắp phóng
- **Version 2**: Kích hoạt khóa an toàn
- **Version 3**: Bắn ngư lôi

---

## 🛠️ Giai Đoạn Xây Dựng (Construction Phase)

- Mỗi subsystem được phát triển **lặp lại, độc lập, song song**.
- Sau mỗi vòng lặp, thực hiện **kiểm thử tích hợp** để kiểm tra giao tiếp giữa các subsystem.
- Đảm bảo các **interface hoạt động đúng như thiết kế Facade**.

---

## 🧠 Tóm Tắt

Để quản lý hệ thống lớn và phức tạp hiệu quả:

- 💡 **Dùng Package UML** để chia nhỏ hệ thống thành các phần dễ kiểm soát.
- 🧩 **Tổ chức theo hướng kiến trúc** với nhóm kiến trúc riêng quản lý toàn cục.
- 🧱 **Áp dụng mẫu Facade** để giảm phụ thuộc chéo và tăng khả năng thay thế.
- ⛓️ **Chia nhỏ Use Case** và xây dựng theo vòng lặp nhỏ, rõ ràng.
- 👥 **Phát triển song song** giữa các nhóm subsystem.

> ✅ Kết hợp các kỹ thuật này giúp giữ sự linh hoạt của Iterative và Incremental Framework ngay cả trong dự án lớn.
