---
layout: post
title: Lập trình hướng đối tượng trong Python
description: Các tính năng của lập trình hướng đối tượng (OOP) trong Python giúp dễ dàng xây dựng các chương trình có độ phức tạp ngày càng tăng và tái sử dụng lại các thành phần đã tồn tại trong quá trình phát triển.
keywords: lập trình OOP trong ngôn ngữ Python, lập trình oop, ngôn ngữ Python, lập trình hướng đối tượng, Object Oriented Programming, lập trình oop trong python, oop trong lập trình python, tính chất oop, python, lập trình python, oop trong python, lập trình hướng đối tượng trong python
excerpt: Các tính năng của lập trình hướng đối tượng (OOP) trong Python giúp dễ dàng xây dựng các chương trình có độ phức tạp ngày càng tăng và tái sử dụng lại các thành phần đã tồn tại trong quá trình phát triển.
author: Nguyễn Trường Long
---

### Lập trình hướng đối tượng trong Python

Lập trình hướng đối tượng (Object-oriented programming - OOP) là một mô hình lập trình trong đó khối xây dựng cơ bản (building block) là đối tượng phần mềm (software object). Trong lập trình hướng đối tượng, các chương trình phần mềm được thiết kế theo một mô hình bao gồm các đối tượng và hành vi của đối tượng chứ không phải là các chức năng và logic. Một đối tượng có thể được định nghĩa là một trường dữ liệu có các thuộc tính và hành vi duy nhất. Lập trình hướng đối tượng tập trung vào các đối tượng mà các nhà phát triển muốn thao tác. Cách tiếp cận này trong lập trình rất phù hợp cho các chương trình lớn, phức tạp cần được cập nhật hoặc bảo trì. Việc tổ chức chương trình phần mềm theo mô hình hướng đối tượng làm phương pháp này có lợi cho sự hợp tác theo nhóm trong quá trình phát triển. Các lợi ích bổ sung của lập trình hướng đối tượng bao gồm khả năng tái sử dụng mã, khả năng mở rộng và tính hiệu quả.

### Class và Object trong Python

Một object là tập hợp các dữ liệu có hành vi liên quan với nhau. Class giống như một bản vẽ (blueprint) để tạo ra object. Nó là bản thiết kế mô tả chi tiết của một đối tượng. Các object riêng lẻ được tạo từ một định nghĩa chính là class. Theo thuật ngữ trong OOP thuần túy thì object là thể hiện (instance) cụ thể của class. Trong ngôn ngữ lập trình Python, mã lập trình có thể xác định các thuộc tính (attributes) và phương thức (methods). Một class trong ngôn ngữ Python chỉ đơn giản là đại diện của một loại đối tượng (type of object). Class trong Python bao gồm ba thứ là tên, thuộc tính và phương thức. Theo quy ước thì tên class phải bắt đầu bằng một chữ cái viết hoa. 

Khi một định nghĩa class trong Python được khai báo thì một namespace mới được tạo ra và xem như là một phạm vi cục bộ (local scope). Cú pháp định nghĩa class có hai phần: tiêu đề class và tập hợp các định nghĩa phương thức theo sau tiêu đề class. Tiêu đề class bao gồm tên class và tên class cha. Tên class chính là một định danh trong Python (Python identifier).

### Các tính chất OOP trong Python

#### Tính thừa kế (inheritance)

Thừa kế là mối quan hệ được biết đến nhiều nhất và được sử dụng rất nhiều trong lập trình hướng đối tượng. Chúng ta có thể hình dung thừa kế giống như một cây gia phả trong gia đình. Các thế sau thừa kế đặc điểm từ các thế hệ trước trong gia đình và cũng có những đặc điểm riêng biệt. Trong lập trình hướng đối tượng, các class có thể sử dụng lại mã nguồn từ các class khác. Tính chất này của OOP buộc phải phân tích dữ liệu kỹ lưỡng hơn, giảm thời gian phát triển và đảm bảo mức độ chính xác cao hơn.

##### Đa thừa kế (multiple inheritance)

Trong lập trình hướng đối tượng, thay vì kế thừa các tính năng và phương thức từ một class duy nhất, một class có thể kế thừa các thuộc tính và phương thức từ nhiều class cha khác nhau.

##### Method Overriding trong Python 

#### Tính đa hình (polymorphism)

Trong lập trình hướng đối tượng (OOP), đa hình (polymorphism) là một tính chất cho phép sử dụng các phương thức (method) của một class con với các đối tượng của các class khác nhau.

Trong Python, đa hình có thể được thực hiện bằng cách sử dụng phương thức có cùng tên trong các class khác nhau. Khi gọi phương thức, Python sẽ tìm kiếm phương thức có cùng tên trong class của đối tượng và thực thi phương thức đó.

Ví dụ, ta có hai class Animal và Dog. Class Dog là một class con của class Animal, nghĩa là class Dog kế thừa toàn bộ các thuộc tính và phương thức của class Animal.

{% highlight python %}
class Animal:
    def __init__(self, name):
        self.name = name
    
    def sound(self):
        pass

class Dog(Animal):
    def sound(self):
        return "woof"
        
if __name__ == '__main__':
    animal = Animal("Animal")
    animal.sound()
    dog = Dog("Dog")
    dog.sound()
{% endhighlight %}

Ở đây, class Animal có một phương thức sound, nhưng phương thức này không được định nghĩa, nghĩa là khi ta gọi phương thức này từ một đối tượng của class Animal, Python sẽ không thực hiện bất kỳ thao tác nào.

Trong class Dog, ta định nghĩa lại phương thức sound. Khi ta gọi phương thức sound từ một đối tượng của class Dog, Python sẽ thực hiện phương thức này, trả về chuỗi "woof".

Như vậy, đa hình trong Python cho phép ta sử dụng các phương thức của class con với các đối tượng của các class khác nhau, tạo ra tính linh hoạt và tái sử dụng code trong lập trình hướng đối tượng. Các đối tượng được thiết kế để chia sẻ các hành vi và chúng có thể có nhiều dạng. Chương trình sẽ xác định ý nghĩa hoặc cách sử dụng nào là cần thiết cho mỗi lần thực thi đối tượng đó từ một class cha, giảm nhu cầu sao chép mã. Tính đa hình cho phép các loại đối tượng khác nhau đi qua cùng một giao diện. Một class con kế thừa tất cả các phương thức từ class cha. Trong những trường hợp như vậy, chúng ta sẽ phải triển khai lại phương thức trong class con. Tính đa hình trong ngôn ngữ lập trình Python định nghĩa các phương thức trong class con có cùng tên với các phương thức trong class cha. Ngoài ra, có thể sửa đổi một phương thức trong một class con mà nó đã kế thừa từ class cha. Điều này chủ yếu được sử dụng trong trường hợp phương thức kế thừa từ class cha không phù hợp với class con. Quá trình thực hiện lại một phương thức trong class con này được gọi là ghi đè phương thức.

#### Tính trừu tượng (abstraction)

#### Tính đóng gói (encapsulation)

Đóng gói là một trong những khái niệm cơ bản trong lập trình hướng đối tượng. Tính chất này cho phép gói dữ liệu và các phương thức hoạt động trên dữ liệu trong một đơn vị. Điều này tạo ra những hạn chế nhất định trong việc truy cập trực tiếp tới các biến và phương thức, ngăn chặn việc sửa đổi dữ liệu theo cách không mong đợi. Chỉ có thể thay đổi giá trị biến của đối tượng bằng phương thức của đối tượng. Các loại biến kiểu như vậy được gọi là biến riêng tư (private variable).

### Tài liệu tham khảo