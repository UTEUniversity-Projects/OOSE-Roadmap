Xin chào mọi người! Hôm nay, ở bài học hôm nay, chúng ta sẽ nói về một chủ đề rất thú vị trong lập trình hướng đối tượng. Đó là sự khác biệt giữa **Interface** và **Abstract Class**. Khi nào chúng ta nên dùng Interface? Khi nào thì Abstract Class mới là lựa chọn phù hợp? Và cùng tìm hiểu một vài ví dụ nhỏ minh họa của chúng! Hãy cùng mình tìm hiểu nhé!

Đây là hai khái niệm khá "trừu tượng", nhưng nếu hiểu rõ thì bạn sẽ dễ dàng áp dụng vào thiết kế phần mềm. Giờ thì bắt đầu thôi!

Do bài học này chủ yếu là ôn lại để củng cố kiến thức cho các bạn trước khi bước vào UML, nên mình sẽ cố gắng trình bày một cách cô đọng nhất những kiến thức chính của phần này để giúp các bạn có thể dễ nhớ và áp dụng.

## 1. Định nghĩa
### Interface
**Interface** trong Java giống như một "hợp đồng" mà các lớp phải thực hiện. Nó chỉ chứa các phương thức trừu tượng (abstract methods) và hằng số (constants). Khi triển khai "hợp đồng" này thì các đối tượng triển khai bắt buộc phải triển khai các method đã được quy định. Từ Java 8 trở đi, Interface đã "nâng cấp" khi có thêm phương thức mặc định (default methods) và phương thức tĩnh (static methods). Thật tiện lợi phải không nào?

### Abstract Class
**Abstract Class** thì hơi khác một chút. Nó giống như một "bản thiết kế" nhưng có thể cung cấp cả các chi tiết cụ thể (phương thức thông thường) và các phần trừu tượng (phương thức abstract). "Bản thiết kế" này quy định điểm chung về thuộc tính hay method của các đối tượng kế thừa nó, điểm đặc biệt là bạn không thể khởi tạo trực tiếp một Abstract Class.


## 2. Sự khác biệt chính
Chúng ta cùng so sánh để thấy rõ hơn nhé:

| Đặc điểm                  | Interface                                   | Abstract Class                             |
|---------------------------|---------------------------------------------|-------------------------------------------|
| **Từ khóa sử dụng**      | `interface`                                | `abstract class`                          |
| **Kế thừa**              | Một lớp có thể triển khai nhiều interface   | Một lớp chỉ có thể kế thừa một abstract class |
| **Phương thức**           | Chỉ chứa phương thức trừu tượng (trước Java 8) | Có cả phương thức trừu tượng và thông thường |
| **Constructor**           | Không có                                   | Có                                        |
| **Biến**                  | Chỉ chứa hằng số (public static final)     | Có thể chứa biến với mọi mức độ truy cập  |
| **Tốc độ thực thi**       | Nhanh hơn (được tối ưu hóa hơn)            | Chậm hơn                                  |
| **Thích hợp cho**         | Các hành vi chung giữa các lớp không liên quan | Các lớp có mối quan hệ kế thừa            |

Đơn giản vậy thôi, nhưng tuỳ vào trường hợp, bạn sẽ chọn cái nào hợp lý nhất nhé!

## 3. Khi nào nên sử dụng?
### Interface
Bạn nên dùng Interface khi:
- Muốn định nghĩa một tập hợp hành vi mà nhiều lớp (không liên quan) có thể thực hiện. Ví dụ: Bay, bơi, chạy.
- Cần hỗ trợ **đa kế thừa**, vì Java không cho phép đa kế thừa với Abstract Class.

### Abstract Class
Abstract Class thì phù hợp nếu:
- Bạn muốn chia sẻ code giữa các lớp "cùng họ hàng" (liên quan trực tiếp).
- Cần định nghĩa các thuộc tính hoặc phương thức có thể tái sử dụng trong lớp con. Ví dụ: Các loài động vật đều "ăn" và "ngủ".

## 4. Ví dụ minh họa

### Interface
Hãy tưởng tượng bạn đang xây dựng một chương trình về các loài động vật:
```java
public interface Animal {
    void eat();
    void sleep();
}

public class Dog implements Animal {
    @Override
    public void eat() {
        System.out.println("Dog eats bones");
    }

    @Override
    public void sleep() {
        System.out.println("Dog sleeps in a kennel");
    }
}
```
Như bạn thấy, **Dog** chỉ cần thực hiện những hành vi được định nghĩa trong Interface.

### Abstract Class
Nếu các loài động vật có vài điểm chung nhưng mỗi loài lại "ăn" theo cách riêng thì sao?
```java
public abstract class Animal {
    abstract void eat();

    void sleep() {
        System.out.println("This animal sleeps");
    }
}

public class Dog extends Animal {
    @Override
    public void eat() {
        System.out.println("Dog eats bones");
    }
}
```
Ở đây, **Dog** không cần tự định nghĩa hành vi "ngủ" vì nó đã có sẵn từ Abstract Class rồi!

## 5. Tổng kết
Vậy là chúng ta đã hiểu thêm về sự khác biệt giữa Interface và Abstract Class rồi. Tóm lại:
- Nếu bạn cần "đa kế thừa" hoặc các lớp không liên quan cùng thực hiện một hành vi, hãy chọn **Interface**.
- Nếu bạn muốn chia sẻ code và các lớp có mối quan hệ "họ hàng", hãy chọn **Abstract Class**.

Cảm ơn các bạn đã theo dõi! Có câu hỏi nào không? Đừng ngại để lại bình luận nhé! 😊
