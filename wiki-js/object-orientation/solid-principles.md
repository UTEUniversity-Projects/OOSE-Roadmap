# SOLID: Bí mật để code "đỉnh" hơn mỗi ngày!

Chào bạn,  
Hôm nay, hãy tưởng tượng chúng ta ngồi lại, pha tách cà phê và nói chuyện về thứ gì đó vừa ngầu vừa hữu ích cho công việc viết code hằng ngày nhé. Chủ đề chính là: **SOLID**, một tập hợp nguyên tắc giúp chúng ta viết code sạch hơn, dễ bảo trì hơn và, nói thẳng ra, "ngầu" hơn khi làm việc nhóm.  

Nếu bạn từng nghĩ:  
- "Sao code của mình dễ bị lỗi vậy?"  
- "Code này sửa một tí là lan ra cả dự án, phải làm sao đây?"  

Thì đây, **SOLID chính là người bạn đồng hành tuyệt vời**! 😎  

## Vậy SOLID là gì?  
SOLID gồm 5 nguyên tắc "vàng" trong thiết kế phần mềm, đặt nền móng cho code dễ hiểu, dễ mở rộng và dễ bảo trì. Chúng ta cùng đi qua từng nguyên tắc nhé!  

---

### 1. **S**ingle Responsibility Principle (SRP)  
#### "Một lớp chỉ nên có một lý do để thay đổi."  

Hãy nghĩ về nó như việc mỗi người chỉ nên làm một việc cụ thể trong nhóm. Nếu bạn làm cả code backend lẫn thiết kế giao diện, bạn sẽ nhanh chóng mệt mỏi và mắc lỗi.  

**Ví dụ xấu**:  
```java
public class UserService {
    public void addUser() { 
        // Thêm người dùng
    }

    public void sendWelcomeEmail() { 
        // Gửi email chào mừng
    }
}
```  
Ở đây, `UserManager` vừa quản lý người dùng, vừa lo việc gửi email. Không ổn chút nào!  

**Cải thiện**:  
Tách riêng trách nhiệm:  
```java
public class UserService {
    public void addUser() { 
        // Thêm người dùng
    }
}

public class EmailService {
    public void sendWelcomeEmail() { 
        // Gửi email chào mừng
    }
}
```

---

### 2. **O**pen/Closed Principle (OCP)  
#### "Mở rộng được nhưng không sửa đổi."  

Bạn thích thêm tính năng mà không phải đụng vào code cũ chứ? Đây là nguyên tắc dành cho bạn. Code cũ không sửa thì ít lỗi, đúng không? 😉  

**Ví dụ xấu**:  
```java
public class Discount {
    public double calculate(String type) {
        if (type.equals("NEW_YEAR")) {
            return 50;
        } else if (type.equals("BLACK_FRIDAY")) {
            return 70;
        }
        return 0;
    }
}
```  
Ở đây, nếu bạn muốn thêm một dịp giảm giá nào đó thì sao, ví dụ như giảm giá cho cô Thơ chẳng hạn? Hiển nhiên là bạn phải động vào class Discount và chỉnh sửa mã nguồn của nó rồi, nhưng điều này thật sự thì không được hay cho lắm, hãy đọc tiếp để biết được cách giải quyết sao cho thật "ngầu" nhé =))

**Cải thiện**:  
Sử dụng kế thừa:  
```java
public interface Discount {
    double calculate();
}

public class NewYearDiscount implements Discount {
    @Override
    public double calculate() {
        return 50;
    }
}

public class BlackFridayDiscount implements Discount {
    @Override
    public double calculate() {
        return 70;
    }
}
```
Bạn có thể sử dụng một interface để đưa ra các ràng buộc mà các class thực thi phải làm theo (có thể tham khảo lại bài trước). Lúc này thì bạn chỉ cần tạo mới một đối tượng thôi chứ không cần phải can thiệp vào mã nguồn cũ. Trên thực tế, các vấn đề sẽ không đơn giản như thế này đâu nhé!

---

### 3. **L**iskov Substitution Principle (LSP)  
#### "Lớp con phải có thể thay thế lớp cha mà không làm hỏng chương trình."  

Nguyên tắc này nghe thì hơi "trừu tượng", nhưng ý tưởng rất đơn giản: nếu bạn thay lớp cha bằng lớp con, mọi thứ vẫn phải chạy tốt.  



---

### 4. **I**nterface Segregation Principle (ISP)  
#### "Không nên bắt ai đó dùng những thứ họ không cần."  

Nếu bạn tạo ra một interface quá lớn, các lớp triển khai sẽ phải "gánh" những thứ không liên quan.  

**Ví dụ xấu**:  
```java
public interface Worker {
    void work();
    void eat();
}

public class Robot implements Worker {
    @Override
    public void work() { 
        // Làm việc
    }

    @Override
    public void eat() { 
        // ??? Robot đâu có ăn!
    }
}
```  

**Cải thiện**:  
Tách interface:  
```java
public interface Worker {
    void work();
}

public interface Eater {
    void eat();
}
```

Trên đây là cách giải quyết dựa trên tư tưởng của **ISP**, tuy nhiên bạn cũng đừng nên lạm dụng quá nhé, bởi vì như bạn thấy đấy, cách giải quyết này có một nhược điểm đó chính là sản sinh ra nhiều interface nên nếu không khéo léo thì dễ gây ra sự thừa thải trong mã nguồn. Vậy nên hãy cẩn thận khi sử dụng nhé!

---

### 5. **D**ependency Inversion Principle (DIP)  
#### "Code nên phụ thuộc vào abstraction, không phụ thuộc vào implementation."  

Nghe hơi phức tạp, nhưng bạn chỉ cần nhớ: thay vì code phụ thuộc vào chi tiết cụ thể, hãy để nó dựa vào cái tổng quát.  


---

## Lời kết  

Bạn thấy đó, nguyên tắc SOLID không hề "đáng sợ" như tên gọi. Nó giống như những bài học nhỏ, giúp bạn trở thành một lập trình viên thông minh hơn mỗi ngày. Để áp dụng được tốt SOLID trong quá trình code của mình, không phải ngày một ngày hai mà được nhé, nó sẽ dần tích hợp vào khả năng của bạn trong quá trình phát triển.

Vậy, bạn đã sẵn sàng áp dụng SOLID vào code của mình chưa? Cùng thử ngay và xem sự khác biệt nhé! 🚀
