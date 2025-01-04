### 1. Nguyên lý Low Coupling là gì?

- **Low Coupling** là một nguyên lý quan trọng trong thiết kế phần mềm, nhằm giảm thiểu sự phụ thuộc giữa các module hoặc lớp trong hệ thống. Mục tiêu của Low Coupling là giúp các phần của phần mềm có thể hoạt động độc lập mà không ảnh hưởng lẫn nhau. Khi coupling thấp, việc thay đổi hoặc mở rộng một phần của hệ thống sẽ không làm gián đoạn các phần khác, tạo ra sự linh hoạt và dễ bảo trì. Nguyên lý này không chỉ giúp phần mềm dễ dàng kiểm thử và tái sử dụng mà còn hỗ trợ việc mở rộng và phát triển hệ thống trong tương lai mà không gặp phải những rủi ro do các sự phụ thuộc phức tạp.

- Hãy xem xét ví dụ sau:
  Hệ thống gửi tin nhắn có hai loại là SMS và Email:
  - SMS: Gửi tin nhắn qua điện thoại.
  - Email: Gửi email đến người dùng.
- Cần thiết kế sao cho hệ thống dễ mở rộng (thêm các loại tin nhắn khác) và đạt Low Coupling.

- Dưới đây là triển khai code bằng ngôn ngữ lập trình Java với **High Coupling**:

```
// Lớp gửi SMS
class SMSMessage {
    public void sendSMS(String recipient, String content) {
        System.out.println("Sending SMS to " + recipient + ": " + content);
    }
}

// Lớp gửi Email
class EmailMessage {
    public void sendEmail(String recipient, String content) {
        System.out.println("Sending Email to " + recipient + ": " + content);
    }
}

// Lớp MessageService
class MessageService {
    private SMSMessage smsMessage = new SMSMessage();
    private EmailMessage emailMessage = new EmailMessage();

    public void sendSMS(String recipient, String content) {
        smsMessage.sendSMS(recipient, content);
    }

    public void sendEmail(String recipient, String content) {
        emailMessage.sendEmail(recipient, content);
    }
}

// Main sử dụng MessageService
public class Main {
    public static void main(String[] args) {
        MessageService service = new MessageService();

        // Gửi SMS
        service.sendSMS("1234567890", "Hello via SMS!");

        // Gửi Email
        service.sendEmail("user@example.com", "Hello via Email!");
    }
}
```

- **Giải thích đoạn code trên:**

  - Class `SMSMessage` có chức năng thực hiện gửi tin nhắn thông qua SMS.
  - Class `EmailMessage` có chức năng thực hiện gửi tin nhắn thông qua Email.
  - Class `MessageService` có chức năng thực hiện tạo các đối tượng từ `SMSMessage`, `EmailMessage` và tạo 2 phương thức gửi Message tương ứng.
  - Class `Main` chứa phương thức main thực hiện tạo đối tượng từ `MessageService` và thực hiện 2 phương thức gửi `Message`.

- **Dễ thấy vấn đề gặp phải với High Coupling:**

  - **Sự phụ thuộc cao:**
    - `MessageService` phụ thuộc trực tiếp vào các lớp `SMSMessage` và `EmailMessage`.
    - Nếu thêm loại tin nhắn mới (ví dụ: Push Notification), phải sửa đổi `MessageService`.
  - **Khó mở rộng:** Khi thêm loại tin nhắn, phải thay đổi mã nguồn của MessageService, vi phạm nguyên tắc **Open/Closed**.

  - **Khó kiểm thử:** Không thể kiểm thử MessageService độc lập mà không cần đến các lớp `SMSMessage` hoặc `EmailMessage`.
  - **Không linh hoạt:** `MessageService` bị ràng buộc chặt chẽ với cách triển khai của từng loại tin nhắn.

- **Cách giải quyết:**

  - [**Dependency Injection**](https://gpcoder.com/4975-huong-dan-java-design-pattern-dependency-injection/): Các module không giao tiếp trực tiếp với nhau, mà thông qua interface. Module cấp thấp sẽ implement interface, module cấp cao sẽ gọi module cấp thấp thông qua interface. Dưới đây là code sau khi áp dụng Dependency Injection:

    ```
    // Interface chung cho các loại Message
    interface Message {
        void send(String recipient, String content);
    }

    // Lớp thực hiện gửi SMS
    class SMSMessage implements Message {
        @Override
        public void send(String recipient, String content) {
            System.out.println("Sending SMS to " + recipient + ": " + content);
        }
    }

    // Lớp thực hiện gửi Email
    class EmailMessage implements Message {
        @Override
        public void send(String recipient, String content) {
            System.out.println("Sending Email to " + recipient + ": " + content);
        }
    }

    // Lớp sử dụng Message
    class MessageService {
        private Message message;

        public MessageService(Message message) {
            this.message = message;
        }

        public void sendMessage(String recipient, String content) {
            message.send(recipient, content);
        }
    }

    public class Main {
        public static void main(String[] args) {
            // Gửi SMS
            Message sms = new SMSMessage();
            MessageService smsService = new MessageService(sms);
            smsService.sendMessage("1234567890", "Hello via SMS!");

            // Gửi Email
            Message email = new EmailMessage();
            MessageService emailService = new MessageService(email);
            emailService.sendMessage("user@example.com", "Hello via Email!");
        }
    }
    ```

    - Trong đoạn code trên, ta sẽ sử dụng tạo một **interface** `Message` chứa phương thức trừu tượng là `sendMessage`. Hai class `SMSMessage` và `EmailMessage` sẽ implements **interface** `Message` và `Override` lại phương thức `sendMessage` sao cho phù hợp với mục đích của từng class.

    - Class `MessageService` sẽ đảm nhận việc thực thi phương thức gửi tin nhắn, nhưng ở đây sẽ không sử dụng `SMSMessage` và `EmailMessage` để khởi tạo trực tiếp đối tượng mà sẽ dùng **interface** `Message` là thuộc tính trong `MessageService`. Tại sao? Bởi vì **interface** cho phép chúng ta áp dụng tính đa hình trong **OOP**.

    - Trong Class Main, phương thức main sẽ lần lượt thực hiện:

    - Tạo đối tượng `sms` từ Class `SMSMessage`.
    - Tạo đối tượng `smsService` từ Class `MessageService`.
    - Đối tượng `smsService` thực hiện gọi phương thức `sendMessage`.

    - Tạo đối tượng `email` từ Class `EmailMessage`.
    - Tạo đối tượng `emailService` từ Class `MessageService`.
    - Đối tượng `emailService` thực hiện gọi phương thức `sendMessage`.

    - Dễ thấy, chúng ta có thể dễ dàng tùy biến loại `Message` mà đối tượng được tạo từ `MessageService` sẽ thực thi, từ đó dễ dàng thêm các loại `Message` khác.

  - [**The Law of Demeter**](https://www.geeksforgeeks.org/law-of-demeter-in-java-principle-of-least-knowledge/): Luật này còn được biết đến với tên **Don't talk to strangers** là một phương pháp hữu hiệu để chống lại coupling. Luật này nói rằng bất kỳ phương thức nào của một đối tượng chỉ nên gọi các phương thức thuộc về:
    - Chính nó (Itself).
    - Bất kỳ tham số nào được truyền vào phương thức.
    - Bất kỳ đối tượng nào mà nó tạo ra.
    - Bất kỳ đối tượng thành phần nào mà nó trực tiếp nắm giữ.

### 2. Lợi ích của nguyên lý Low Coupling

- **Tăng tính linh hoạt:** Các lớp ít phụ thuộc vào nhau, giúp việc thay đổi hoặc mở rộng một lớp không ảnh hưởng lớn đến các lớp khác. Khi bạn cần thay đổi một phần của hệ thống, ít có nguy cơ gây lỗi cho các phần khác.
- **Dễ bảo trì và mở rộng:** Với **Low Coupling**, các lớp có thể được thay thế hoặc cải tiến mà không ảnh hưởng đến toàn bộ hệ thống. Điều này giúp bảo trì dễ dàng hơn và việc mở rộng phần mềm trở nên nhanh chóng hơn.
- **Tái sử dụng mã nguồn:** Các lớp ít liên kết với nhau, nên chúng có thể được tái sử dụng trong các phần khác của hệ thống hoặc trong các dự án khác mà không cần phải thay đổi nhiều.
- **Giảm độ phức tạp:** Giảm sự phụ thuộc giữa các lớp giúp giảm độ phức tạp trong hệ thống. Mỗi lớp sẽ chỉ cần hiểu rõ các lớp liên quan trực tiếp của mình, giúp mã nguồn dễ đọc và dễ hiểu hơn.
- **Cải thiện khả năng kiểm thử (Testing):** Với các lớp ít phụ thuộc vào nhau, việc kiểm thử các phần của hệ thống trở nên dễ dàng hơn. Bạn có thể kiểm thử từng lớp độc lập mà không cần phải lo lắng về những lớp khác.
- **Hỗ trợ các mô hình thiết kế hướng đối tượng:** **Low Coupling** giúp các mô hình thiết kế hướng đối tượng (như SOLID, Design Patterns) hoạt động hiệu quả hơn. Nó tạo điều kiện cho việc áp dụng các nguyên lý thiết kế như **Single Responsibility Principle** và **Open/Closed Principle**.
- **Giảm sự thay đổi không mong muốn:** Khi các lớp ít liên kết với nhau, việc thay đổi một lớp sẽ không kéo theo việc thay đổi nhiều lớp khác, giúp giảm rủi ro khi thay đổi phần mềm.

### 3. Một số vấn đề cần xem xét thêm:

- **Không bao giờ làm thuộc tính của lớp trở thành public:** Một thuộc tính public sẽ ngay lập tức mở ra cơ hội cho việc lạm dụng lớp (ngoại lệ là các hằng số mà lớp lưu trữ).
- **Chỉ cung cấp phương thức get/set khi thật sự cần thiết:** Đảm bảo rằng các phương thức này chỉ xuất hiện khi không có cách nào khác để truy cập dữ liệu.
- **Cung cấp public interface tối thiểu:** Chỉ nên làm phương thức trở thành public khi nó thực sự cần thiết cho việc truy cập từ bên ngoài hệ thống.
- **Không để dữ liệu _chảy_ khắp hệ thống:** Giảm thiểu dữ liệu truyền qua các tham số giữa các lớp và phương thức.
- **Không xem xét coupling một cách riêng biệt:** Hãy nhớ nguyên lý **High Cohesion** và **Expert**! Một hệ thống hoàn toàn không có coupling sẽ dẫn đến việc các lớp bị phình to và làm quá nhiều việc, thường thể hiện qua việc hệ thống chỉ có một vài đối tượng hoạt động mà không có sự giao tiếp với nhau.

### 4. Kết luận

- Bằng cách áp dụng Nguyên lý Low Coupling, chúng ta có thể dễ dàng thay đổi nội bộ của các module mà không lo ngại tác động đến các module khác trong hệ thống. Các module này không chỉ dễ tái sử dụng mà còn có thể ghép lại với nhau một cách linh hoạt. Các vấn đề cũng được cô lập trong các đơn vị mã nhỏ gọn, tự chứa và dễ dàng phát triển. Tuân thủ các nguyên lý này giúp phần mềm trở nên mạnh mẽ, linh hoạt và dễ dàng mở rộng.
