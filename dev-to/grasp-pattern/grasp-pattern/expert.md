# Nguyên Lý Expert Trong GRASP Pattern  

## 📖 **Nguyên Lý Expert Là Gì?**  

Nguyên lý **Expert** là một trong những nguyên tắc quan trọng nhất trong tập hợp GRASP Patterns (General Responsibility Assignment Software Patterns). Nguyên tắc này hướng dẫn cách phân bổ trách nhiệm trong các lớp để đảm bảo thiết kế phần mềm tối ưu.  

Nguyên lý này trả lời câu hỏi:  
**"Hành vi này nên được phân bổ vào lớp nào?"**  

Theo nguyên lý Expert:  
- Trách nhiệm nên được giao cho lớp **có đủ thông tin cần thiết** để thực hiện nhiệm vụ. 

### **Lợi Ích Của Nguyên Lý Expert**  
1. **Hệ Thống Dễ Hiểu:** Thiết kế rõ ràng giúp dễ dàng đọc và hiểu mã nguồn.  
2. **Tăng Khả Năng Tái Sử Dụng:** Các lớp được thiết kế đúng trách nhiệm có thể dễ dàng tái sử dụng.  
3. **Dễ Duy Trì:** Mỗi lớp chỉ chịu trách nhiệm về dữ liệu mà nó quản lý.  
4. **Giảm Phụ Thuộc:** Tránh việc các lớp phải truy cập quá nhiều dữ liệu từ các lớp khác.  

---

## 🎯 **Ví Dụ Minh Họa**  

### **Bài Toán**  
Hệ thống quản lý đơn hàng cần tính tổng giá trị của một đơn hàng. Hệ thống gồm các lớp:  
1. **Purchase Order:** Đại diện cho đơn hàng.  
2. **Order Line:** Chi tiết từng dòng sản phẩm trong đơn hàng.  
3. **SKU:** Lưu thông tin sản phẩm, như giá sản phẩm.  

### **Phân Tích Bài Toán Theo Nguyên Lý Expert**  
- Để tính tổng giá trị đơn hàng, cần biết:  
  - Giá trị của từng dòng sản phẩm (`subtotal`).  
  - Giá của từng sản phẩm (`price`).  

- Theo nguyên lý Expert:  
  - Lớp **Purchase Order** chịu trách nhiệm tính tổng giá trị đơn hàng (`calculate_total`).  
  - Lớp **Order Line** chịu trách nhiệm tính giá trị riêng của từng dòng (`subtotal`).  
  - Lớp **SKU** chịu trách nhiệm cung cấp giá sản phẩm (`price`).  

### **Thiết Kế Hệ Thống**  

#### **Các Thành Phần Trong Thiết Kế**  
- **Purchase Order:**  
  - Chứa danh sách các dòng sản phẩm.  
  - Chịu trách nhiệm tính tổng giá trị (`calculate_total()`).  
- **Order Line:**  
  - Chịu trách nhiệm tính giá trị riêng của từng dòng (`subtotal()`).  
  - Lấy thông tin từ đối tượng SKU.  
- **SKU:**  
  - Cung cấp giá sản phẩm (`price()`).  

#### **Luồng Hoạt Động**  
1. **Purchase Order** gọi phương thức `calculate_total()`.  
2. `calculate_total()` lặp qua các dòng sản phẩm trong danh sách và gọi `subtotal()` của **Order Line**.  
3. `subtotal()` sử dụng giá của sản phẩm từ **SKU** để tính toán.  

---

## 🌐 **Lợi Ích Của Thiết Kế Theo Nguyên Lý Expert**  

1. **Phân Bổ Trách Nhiệm Hợp Lý:**  
   - Mỗi lớp xử lý đúng trách nhiệm dựa trên thông tin mà nó quản lý.  

2. **Giảm Phụ Thuộc (Low Coupling):**  
   - Lớp **Purchase Order** không cần biết chi tiết giá sản phẩm, mà chỉ cần gọi phương thức từ **Order Line**.  

3. **Tăng Tính Tái Sử Dụng:**  
   - Lớp **Order Line** và **SKU** có thể tái sử dụng trong các ngữ cảnh khác, ví dụ như hệ thống phân tích bán hàng.  

4. **Dễ Duy Trì:**  
   - Thay đổi một thành phần, như cách tính giá trong **SKU**, sẽ không ảnh hưởng đến các lớp khác.  

---

## 🛑 **Một Số Lưu Ý Khi Áp Dụng Nguyên Lý Expert**  

1. **Tránh Phụ Thuộc Không Cần Thiết:**  
   - Không để lớp quản lý dữ liệu của lớp khác, dẫn đến việc vi phạm nguyên lý.  

2. **Đừng Lạm Dụng:**  
   - Không phải lúc nào cũng nên giao toàn bộ trách nhiệm cho một lớp. Đôi khi cần tách nhỏ trách nhiệm để đảm bảo tính linh hoạt.  

3. **Kết Hợp Với Nguyên Lý Khác:**  
   - Sử dụng **Low Coupling** để giảm mối quan hệ chặt chẽ giữa các lớp.  
   - Dùng **High Cohesion** để giữ trách nhiệm của từng lớp tập trung vào một mục tiêu cụ thể.  

---

## ✨ **Kết Luận**  

Nguyên lý **Expert** trong GRASP giúp bạn xây dựng các lớp với trách nhiệm rõ ràng và hợp lý. Thiết kế theo nguyên lý này không chỉ làm giảm độ phức tạp của hệ thống mà còn tăng khả năng tái sử dụng và bảo trì.  

Hãy áp dụng Expert để đảm bảo mỗi lớp trong hệ thống của bạn đều hoạt động hiệu quả và đúng với vai trò của nó!  

>**Hãy giữ mọi thứ thật rõ ràng!**
