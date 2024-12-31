# DRY Principle - "Don't Repeat Yourself"

---

## 🤔 Vậy DRY là gì nhỉ?

"DRY" là viết tắt của **"Don't Repeat Yourself"**, một nguyên tắc vàng trong lập trình (và cả trong cuộc sống nữa đó!). Ý tưởng rất đơn giản: **"Đừng lặp lại chính mình."** 

Hãy tưởng tượng bạn viết một công thức nấu ăn mà phải copy-paste từng bước mỗi khi làm một món ăn khác. Lỡ bạn muốn thêm muối, bạn sẽ phải cập nhật từng bản copy. Ngán chưa? Đó chính là "lặp lại" trong lập trình!

---

## DRY dưới góc nhìn lập trình

Nguyên tắc DRY yêu cầu bạn **cô lập logic** hoặc đoạn mã thường lặp lại vào một vị trí duy nhất. Khi cần thay đổi, bạn chỉ việc sửa một nơi mà không cần tìm từng dòng để sửa.

### ✔ Ví dụ:
Bạn đang viết một ứng dụng quản lý thú cưng:

#### Trước khi áp dụng DRY:
```java
public void feedDog() {
    System.out.println("Feeding the dog");
}

public void feedCat() {
    System.out.println("Feeding the cat");
}

public void feedParrot() {
    System.out.println("Feeding the parrot");
}
```
Cứ thêm thú cưng là bạn phải viết thêm một phương thức mới. Thật phiền phức đúng không nào? 🙈

```java
public void feedAnimal(String animal) {
    System.out.println("Feeding the " + animal);
}
```
Bây giờ, bạn chỉ cần gọi `feedAnimal("dog")`, `feedAnimal("cat")` mà không lo lặp lại đoạn code y chang nhau! Tiết kiệm thời gian, giảm đau đầu. 🥳

---

## DRY trong thực tế
DRY không chỉ giúp bạn viết code "ngầu" hơn mà còn cải thiện khả năng bảo trì và mở rộng ứng dụng.

### ✔ Một ví dụ thực tế:
Giả sử bạn xây dựng một website và phải sử dụng cùng một đoạn HTML cho phần footer:

```html
<div class="footer">
    <p>Contact us at: congquynguyen@gmail.com</p>
</div>
```
**Trước DRY**:
Bạn copy-paste đoạn HTML này vào mọi trang. Lỡ email thay đổi? Hoặc đó là một đoạn code dài ơi là dài ? Bạn phải chỉnh sửa từng trang. Quá tốn công!

**Sau DRY**:
Sử dụng một tệp template hoặc component tái sử dụng:
```html
<include src="footer.html"></include>
```

Bây giờ chỉ cần sửa một tệp duy nhất khi có thay đổi. Đơn giản hơn nhiều, đúng không?

---

## Lợi ích khi áp dụng DRY
* *Dễ bảo trì hơn:* Sửa một chỗ thay vì "sửa toàn cầu".
* *Code gọn gàng:* Giảm "sự lộn xộn" và tăng độ đọc hiểu.
* *Ít lỗi hơn:* Mỗi thay đổi đều được áp dụng nhất quán.

## Thách thức khi thực hiện DRY
* *Over-DRY:* Đừng cố DRY mọi thứ! Đôi khi, chia nhỏ quá mức sẽ làm code phức tạp và khó hiểu hơn.
* *Lựa chọn sai ngữ cảnh:* DRY chỉ hiệu quả khi áp dụng đúng lúc, đúng chỗ. Nếu không, nó sẽ trở thành một "cơn ác mộng bảo trì."

---

## Tóm lại
Nguyên tắc DRY là một trong những "bí kíp" giúp bạn trở thành lập trình viên chuyên nghiệp. Tuy nhiên, hãy nhớ rằng cân bằng là chìa khóa. Không phải lúc nào DRY cũng là giải pháp tốt nhất, nhưng khi áp dụng đúng, nó sẽ giúp bạn tiết kiệm cả thời gian và năng lượng! 💪