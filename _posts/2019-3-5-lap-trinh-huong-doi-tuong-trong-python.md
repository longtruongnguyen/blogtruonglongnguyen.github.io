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

Thừa kế là mối quan hệ được biết đến nhiều nhất và được sử dụng rất nhiều trong lập trình hướng đối tượng. Tính kế thừa (Inheritance) trong lập trình hướng đối tượng là một tính năng cho phép một đối tượng (object) kế thừa tất cả các thuộc tính và phương thức của đối tượng cha (parent object). Tính kế thừa cho phép xây dựng các class mới dựa trên các class đã có sẵn, giúp tái sử dụng mã nguồn và tăng tính tái sử dụng. Chúng ta có thể hình dung thừa kế giống như một cây gia phả trong gia đình. Các thế sau thừa kế đặc điểm từ các thế hệ trước trong gia đình và cũng có những đặc điểm riêng biệt. Trong lập trình hướng đối tượng, các class có thể sử dụng lại mã nguồn từ các class khác.

Trong tính kế thừa, class con (subclass) được xây dựng dựa trên class cha (superclass) và sẽ có tất cả các thuộc tính và phương thức của class cha. Class con có thể mở rộng hoặc ghi đè (override) các phương thức hoặc thuộc tính của class cha và có thể thêm các phương thức hoặc thuộc tính mới.

Ví dụ, chúng ta có thể có class cha là class Animal (Động vật) với các thuộc tính và phương thức như tên, tuổi, cân nặng, ăn, uống và di chuyển. Chúng ta có thể tạo class con là class Dog (Chó) và kế thừa các thuộc tính và phương thức của class Animal, sau đó định nghĩa thêm các thuộc tính và phương thức mới như lúc sủa, đuổi bắt và liếm chủ.

{% highlight python %}
class Animal:
    def __init__(self, name, age, weight):
        self.name = name
        self.age = age
        self.weight = weight

    def eat(self):
        print("Animal is eating")

    def drink(self):
        print("Animal is drinking")

    def move(self):
        print("Animal is moving")

class Dog(Animal):
    def __init__(self, name, age, weight, breed):
        super().__init__(name, age, weight)
        self.breed = breed

    def bark(self):
        print("Dog is barking")

    def chase(self):
        print("Dog is chasing")

    def lick_owner(self):
        print("Dog is licking its owner")
{% endhighlight %}

Trong ví dụ trên, class Dog kế thừa tất cả các thuộc tính và phương thức của class Animal, và có thêm các thuộc tính và phương thức riêng như breed, bark, chase và lick_owner. Bằng cách sử dụng tính kế thừa, chúng ta có thể sử dụng lại mã nguồn đã được định nghĩa trong class Animal và mở rộng hoặc ghi đè phương thức và thuộc tính để tạo ra class con mới.

Tính chất này của OOP buộc phải phân tích dữ liệu kỹ lưỡng hơn, giảm thời gian phát triển và đảm bảo mức độ chính xác cao hơn.

##### Đa thừa kế (multiple inheritance)

Trong lập trình hướng đối tượng, thay vì kế thừa các tính năng và phương thức từ một class duy nhất, một class có thể kế thừa các thuộc tính và phương thức từ nhiều class cha khác nhau. Ví dụ, giả sử chúng ta có 2 class cha là Employee và Person, và chúng ta muốn tạo một class con Manager kế thừa từ cả 2 class cha này. Trong Python, ta có thể định nghĩa class Manager như sau:

{% highlight python %}
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

class Employee:
    def __init__(self, salary):
        self.salary = salary

class Manager(Person, Employee):
    def __init__(self, name, age, salary):
        Person.__init__(self, name, age)
        Employee.__init__(self, salary)
        
if __name__ == '__main__':
    manager = Manager('John Doe', 35, 5000)
    print(manager.name) # Output: John Doe
    print(manager.salary) # Output: 5000
{% endhighlight %}

Trong đó, class Manager được khai báo kế thừa từ cả Person và Employee bằng cách đưa chúng vào trong dấu ngoặc đơn của từ khóa class. Từ đó, class Manager có thể truy cập vào các thuộc tính và phương thức của cả class Person và class Employee.

Tính đa thừa kế có thể giúp chúng ta dễ dàng tái sử dụng lại mã nguồn code, tuy nhiên nó cũng có thể gây ra những rắc rối về quản lý, đặc biệt là khi có nhiều class cha chia sẻ các thuộc tính và phương thức giống nhau. Do đó, việc sử dụng tính đa thừa kế cần được thận trọng và cân nhắc kỹ lưỡng.

##### Method Overriding trong Python 

Method overriding là một tính năng của lập trình hướng đối tượng cho phép class con ghi đè lên phương thức của class cha và triển khai lại phương thức đó với cùng tên và cùng số lượng tham số. Khi đối tượng class con gọi phương thức đã được ghi đè, phương thức sẽ được triển khai từ class con chứ không phải class cha.

Ví dụ, ta có class cha Animal và class con Cat. Class Animal có phương thức make_sound, trong khi class Cat cũng có phương thức này, nhưng khi class con ghi đè phương thức make_sound, phương thức sẽ được triển khai từ class Cat thay vì từ class Animal.

{% highlight python %}
class Animal:
    def make_sound(self):
        print("Animal is making a sound...")

class Cat(Animal):
    def make_sound(self):
        print("Meow")

cat = Cat()
cat.make_sound() # output: Meow
{% endhighlight %}

Ở đây, phương thức make_sound của class Cat đã ghi đè lên phương thức make_sound của class Animal. Khi gọi phương thức make_sound trên đối tượng cat, kết quả sẽ là "Meow" thay vì "Animal is making a sound...".

##### Method Overloading trong Python

Method overloading là một tính năng trong lập trình hướng đối tượng cho phép một lớp có nhiều phương thức cùng tên nhưng có các đối số khác nhau. Khi gọi phương thức, trình thông dịch hoặc biên dịch sẽ xác định phương thức phù hợp dựa trên số lượng và kiểu dữ liệu của các đối số được truyền vào.

Tính năng này giúp cho việc định nghĩa phương thức trở nên linh hoạt hơn, tiết kiệm thời gian và giảm sự trùng lặp code. Tuy nhiên, nó không được hỗ trợ trong một số ngôn ngữ lập trình như Python chẳng hạn. Trong Python, không có hỗ trợ cho method overloading như trong một số ngôn ngữ truyền thống khác. Thay vào đó, Python hỗ trợ tính năng tương tự thông qua tính đa hình (polymorphism) và định nghĩa các tham số mặc định của phương thức. Xem xét các ví dụ sau với định nghĩa một phương thức add() với một tham số và một phương thức add() khác với hai tham số:

{% highlight python %}
class Calculator:
    def add(self, a):
        return a + 1
    
    def add(self, a, b):
        return a + b

if __name__ == '__main__':
    c = Calculator()
    print(c.add(1))
    print(c.add(2, 3))
{% endhighlight %}

Khi chúng ta gọi phương thức add() với một tham số sẽ phát sinh lỗi, do Python chỉ gọi đến phương thức add() được định nghĩa cuối cùng là phương thức add() với hai tham số. Phương thức add() với một tham số đã bị ghi đè bởi phương thức add() với hai tham số. Và từ đó chúng ta sẽ nhận được kết quả không như mong muốn. Vì vậy, thay vì sử dụng method overloading, chúng ta có thể tận dụng các tính năng khác của Python để đạt được mục đích tương tự.

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

Tính trừu tượng (abstraction) là một khái niệm quan trọng trong lập trình hướng đối tượng. Tính chất này cho phép người lập trình tập trung vào việc định nghĩa các đối tượng và thuộc tính của chúng, thay vì các chi tiết bên trong hoạt động của chúng. Nó giúp giảm sự phức tạp của các đối tượng và cho phép các đối tượng được sử dụng ở nhiều nơi trong chương trình mà không cần biết chi tiết bên trong của chúng.

Tính trừu tượng có thể được thực hiện thông qua các class trừu tượng (abstract class) và phương thức trừu tượng (abstract method). Class trừu tượng là một class mà không thể tạo ra các đối tượng trực tiếp từ đó, mà chỉ được sử dụng để định nghĩa các thuộc tính và phương thức cho các lớp con của nó. Phương thức trừu tượng là một phương thức mà chỉ có định nghĩa và không có cài đặt cụ thể cho phương thức đó.

Ví dụ, giả sử chúng ta đang xây dựng một ứng dụng quản lý thư viện và chúng ta muốn định nghĩa một class trừu tượng "Đầu sách" để đại diện cho tất cả các đầu sách có sẵn trong thư viện. Class này có thể định nghĩa các thuộc tính chung cho tất cả các đầu sách, chẳng hạn như mã ISBN, tên tác giả và năm xuất bản. Các class con của "Đầu sách", chẳng hạn như "Sách giáo khoa" và "Sách văn học", có thể mở rộng lớp cha này bằng cách thêm các thuộc tính và phương thức đặc biệt của riêng chúng.

Ví dụ về lớp trừu tượng:

{% highlight python %}
from abc import ABC, abstractmethod

class Book(ABC):
    def __init__(self, isbn, author, year):
        self.isbn = isbn
        self.author = author
        self.year = year

    @abstractmethod
    def get_title(self):
        pass

class Textbook(Book):
    def __init__(self, isbn, author, year, subject):
        super().__init__(isbn, author, year)
        self.subject = subject

    def get_title(self):
        return f"{self.subject} textbook"

class Novel(Book):
    def __init__(self, isbn, author, year, genre):
        super().__init__(isbn, author, year)
        self.genre = genre

    def get_title(self):
        return f"{self.genre} novel"
{% endhighlight %}

#### Tính đóng gói (encapsulation)

Đóng gói là một trong những khái niệm cơ bản và là một tính chất quan trọng trong lập trình hướng đối tượng. Tính chất này giúp che dấu thông tin của đối tượng, bao gồm các thuộc tính (attributes) và phương thức (methods), để người dùng không thể truy cập và thay đổi chúng trực tiếp, ngăn chặn việc sửa đổi dữ liệu theo cách không mong đợi. Chỉ có thể thay đổi giá trị thuộc tính của đối tượng bằng phương thức của đối tượng.

Trong Python, tính đóng gói cũng được thực hiện bằng cách che dấu thông tin các thuộc tính (attributes) và phương thức (methods) của một đối tượng. Có ba cấp độ của tính đóng gói trong lập trình hướng đối tượng của Python là public, protected và private.

##### 1. Public

Ở cấp độ public thì thuộc tính hoặc phương thức có thể truy cập từ bên ngoài đối tượng và từ bất kỳ đối tượng nào khác trong cùng module hoặc package. Trong Python, các thuộc tính và phương thức được định nghĩa mặc định là public.

Ví dụ:

{% highlight python %}
class Person:
    def __init__(self, name, age):
        self.name = name  # public attribute
        self.age = age    # public attribute
        
    def say_hello(self): # public method
        print(f"Hello, my name is {self.name}.")
{% endhighlight %}

##### 2. Protected

Ở cấp độ protected thì thuộc tính hoặc phương thức chỉ có thể truy cập từ bên trong đối tượng và từ các đối tượng con kế thừa từ đối tượng đó. Trong Python, để định nghĩa thuộc tính hoặc phương thức ở cấp độ này, chúng ta thêm dấu gạch dưới đầu tiên trước tên thuộc tính hoặc phương thức.

Ví dụ:

{% highlight python %}
class Person:
    def __init__(self, name, age):
        self._name = name  # protected attribute
        self._age = age    # protected attribute
        
    def _say_hello(self): # protected method
        print(f"Hello, my name is {self._name}.")
{% endhighlight %}

##### 3. Private

Ở cấp độ private thì thuộc tính hoặc phương thức chỉ có thể truy cập từ bên trong đối tượng, không thể truy cập từ bên ngoài đối tượng và các đối tượng con kế thừa từ đối tượng đó. Trong Python, để định nghĩa thuộc tính hoặc phương thức ở cấp độ này, chúng ta thêm hai dấu gạch dưới đầu tiên trước tên thuộc tính hoặc phương thức.

Ví dụ:

{% highlight python %}
class Person:
    def __init__(self, name, age):
        self.__name = name  # private attribute
        self.__age = age    # private attribute
        
    def __say_hello(self): # private method
        print(f"Hello, my name is {self.__name}.")
{% endhighlight %}


### Tài liệu tham khảo

