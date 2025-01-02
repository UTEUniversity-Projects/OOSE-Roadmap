# Introduction to Object Orientation (OO)

Trong chương này, chúng ta sẽ tìm hiểu về **Object Orientation (OO)** và khám phá những lợi ích mà nó mang lại trong quá trình phát triển hệ thống phần mềm.

#### Tại sao chúng ta lại cần **Object Orientation (OO)** trong **Software Development**?

Để trả lời câu hỏi này, trước tiên, hãy cùng xem xét (một cách sơ lược) cách các hệ thống phần mềm được thiết kế bằng phương pháp **Structured Programming** (hay còn gọi là **Functional Programming**).

## **1. Structured Programming:**

Trong **Structured Programming**, phương pháp chung là phân tích bài toán và chia nhỏ nó thành các **hàm (functions)** để thực hiện các tác vụ cụ thể. Hầu hết các hàm này đều cần một loại dữ liệu để xử lý. Dữ liệu trong một hệ thống **functional** thường được lưu trữ trong _cơ sở dữ liệu_ hoặc có thể được giữ trong bộ nhớ dưới dạng _biến toàn cục (global variables)_.

Lấy một ví dụ đơn giản về một **hệ thống quản lý trường học**. Hệ thống này lưu trữ thông tin chi tiết của tất cả sinh viên và giảng viên trong trường. Đồng thời, nó cũng quản lý thông tin về các khóa học được cung cấp tại trường và theo dõi sinh viên nào đang theo học các khóa học nào.

Hệ thống cần lưu trữ thông tin về **Sinh viên (Student)**, **Giảng viên (Teacher)**, **Kỳ thi (Exam)** và **Khóa học (Course)**, và được thiết kế với các hàm chức năng như:

- `add_student`
- `enter_for_exam`
- `check_exam_marks`
- `issue_certificate`
- `expel_student`

Từ đó, chúng ta có thể xây dựng sơ đồ về các dữ liệu, hàm và sự phụ thuộc như sau:
![Sơ đồ dữ liệu, hàm và sự phụ thuộc](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/w6lghj5a0e0milyi4t4t.png)

Vấn đề với phương pháp này là nếu bài toán chúng ta đang giải quyết trở nên quá phức tạp, hệ thống sẽ ngày càng khó duy trì. Lấy ví dụ trên, điều gì sẽ xảy ra nếu một yêu cầu thay đổi cách thức xử lý dữ liệu của **Student**, chẳng hạn như việc chuyển trường _"năm sinh"_ từ hai chữ số sang bốn chữ số? Chỉ với một thay đổi nhỏ này có thể dẫn đến các **side effects (hiệu ứng phụ)** không lường trước được và gây ra những vấn đề nghiêm trọng. Dữ liệu về **Exam**, **Course** và **Teacher** đều phụ thuộc vào dữ liệu của **Student**. Thêm vào đó, chúng ta có thể đã làm hỏng các hàm `add_student`, `enter_for_exams`, `issue_certificate`, và `expel_student`. Ví dụ, `add_student` chắc chắn sẽ không hoạt động nữa, vì nó sẽ cần dữ liệu hai chữ số cho "năm sinh" thay vì bốn chữ số.

Từ ví dụ trên, chúng ta có thể nhận thấy một số nhược điểm của **Structured Programming**, bao gồm _sự phụ thuộc_ lẫn nhau giữa các hàm và dữ liệu, dẫn đến _khó bảo trì_, _khó mở rộng_ và _dễ gặp phải các vấn đề ngoài ý muốn khi thay đổi dữ liệu_. Để giải quyết những vấn đề này, chúng ta cần một cách tiếp cận mới, và đó chính là **Object Oriented (OO)**.

## **2. Object Oriented:**

### **2.1. Khái niệm:**

> **Object (Đối tượng):** có thể hiểu là một thực thể cụ thể, bao gồm 2 thành phần chính là:
>
> - **Thuộc tính (Attributes)**: Là những thông tin, đặc điểm của đối tượng.
>
> - **Phương thức (Methods)**: Là những thao tác, hành động mà đối tượng có thể thực hiện.

Từ ví dụ về bài toán _hệ thống quản lý trường học_ trên ta có thể có các đối tượng sau:
![Ví dụ về _hệ thống quản lý trường học_](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/pmsyqycgi58qnfnyjyak.png)

> **Class (Lớp):** là một kiểu dữ liệu bao gồm các thuộc tính và phương thức được định nghĩa từ trước mà các đối tượng sẽ có. Chúng ta có thể hiểu class chính là một khuôn mẫu để tạo ra các đối tượng.

_Ví dụ:_ Class **Student** chính là một khuôn mẫu định nghĩa chung cho tất cả sinh viên, bao gồm các thuộc tính và phương thức chung như tên, năm sinh và các hành động như đăng ký học. Còn đối tượng là một sinh viên cụ thể tên là _Nguyễn Văn A sinh năm 2004_ mang các đặc tính của class **Student**

### **2.2. Các nguyên lý cơ bản của OOP:**

#### **Tính đóng gói (Encapsulation)**

> **Tính đóng gói** là việc nhóm các thuộc tính và phương thức có liên quan vào cùng một lớp, nhằm mục đích quản lý và sử dụng một cách hiệu quả. Điều này giúp giảm sự phức tạp và tăng tính bảo mật, đồng thời làm cho mã nguồn dễ duy trì và mở rộng.

```java
public class Student {
    private String name;
    private String dateOfBirth;


    public void registerForCourse(Course course) {
        course.addStudent(this);
    }
}
```

> Thông tin của Student sẽ được đóng gói trong lớp Student, và các hành động liên quan đến Student sẽ được thực hiện thông qua các phương thức trong lớp này.

#### **Tính kế thừa (Inheritance)**

> **Tính kế thừa** cho phép một lớp (class) con kế thừa các thuộc tính và phương thức của lớp cha (class) để tái sử dụng mã nguồn một cách tối ưu và dễ dàng mở rộng chức năng.

```java
public class Person {
    private String name;
    private String dateOfBirth;
}

public class Student extends Person {
    private double gpa;
}

public class Teacher extends Person {
    private String department;
}
```

> **Student** và **Teacher** đều kế thừa từ lớp **Person**, giúp tái sử dụng các thuộc tính chung. Mỗi lớp con có thể bổ sung thêm thuộc tính hoặc phương thức riêng biệt.

#### **Tính đa hình (Polymorphism)**

> **Tính đa hình** cho phép một phương thức có thể được thực hiện bằng nhiều cách khác nhau, tức là phương thức có thể được định nghĩa lại trong lớp con với các hành vi khác nhau.

```java
public class Person {
    public void introduce() {
        System.out.println("I am a person.");
    }
}

public class Student extends Person {
    @Override
    public void introduce() {
        System.out.println("I am a student.");
    }
}

public class Teacher extends Person {
    @Override
    public void introduce() {
        System.out.println("I am a teacher.");
    }
}

public class Main {
    public static void main(String[] args) {
        Person person = new Person();
        Person student = new Student();
        Person teacher = new Teacher();

        person.introduce(); // I am a person.
        student.introduce(); // I am a student.
        teacher.introduce(); // I am a teacher.
    }
}
```

> Phương thức _introduce_ được định nghĩa trong lớp **Person** và ghi đè trong các lớp con **Student** và **Teacher**. Mặc dù sử dụng kiểu **Person**, nhưng khi gọi phương thức _introduce_, hệ thống sẽ sử dụng phương thức phù hợp của đối tượng thực tế (**Student** hoặc **Teacher**), thể hiện tính đa hình.

#### **Tính trừu tượng (Abstraction)**

> **Tính trừu tượng** là một phương pháp làm việc với các khái niệm tổng quát mà không cần phải quá chú trọng đến các chi tiết triển khai cụ thể, giúp tăng tính linh hoạt và giảm sự phức tạp.

```java
abstract class Course {
    private String courseName;

    public abstract void startCourse();
}

class MathCourse extends Course {
    @Override
    public void startCourse() {
        System.out.println("Math course started.");
    }
}

class ScienceCourse extends Course {
    @Override
    public void startCourse() {
        System.out.println("Science course started.");
    }
}

public class Main {
    public static void main(String[] args) {
        Course math = new MathCourse();
        Course science = new ScienceCourse();

        math.startCourse(); // Math course started.
        science.startCourse(); // Science course started.
    }
}
```

> Với **Abstraction**, chúng ta định nghĩa một lớp trừu tượng (**Course**) với các phương thức tổng quát (`startCourse()`). Các lớp con như **MathCourse** và **ScienceCourse** triển khai chi tiết các phương thức này, giúp hệ thống dễ dàng mở rộng và tùy chỉnh.

## **3. Các ưu điểm của lập trình hướng đối tượng:**

- Dễ dàng quản lý và mở rộng dự án nhờ cấu trúc tổ chức mã nguồn logic và chặt chẽ.
- Tối ưu hóa khả năng tái sử dụng mã, hạn chế dư thừa, tiết kiệm thời gian phát triển và nâng cao hiệu quả làm việc.
- Tiết kiệm thời gian và tăng năng suất.
- Khái niệm lớp và đối tượng giúp mô phỏng các thực thể trong thế giới thực một cách tự nhiên và rõ ràng hơn trên máy tính, đồng thời khắc phục các hạn chế của lập trình hướng cấu trúc.
