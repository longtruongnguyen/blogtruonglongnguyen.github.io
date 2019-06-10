---
layout: post
title: Objects trong JavaScript
keywords: "objects trong javaScript, đối tượng object trong javascript, javaScript objects"
---

Trong ngôn ngữ lập trình JavaScript, một object là nơi chứa tập hợp các giá trị và các hàm có liên quan đến nhau. Ví dụ nếu chúng ta đã viết hàm tính chu vi và diện tích của một hình chữ nhật, ta có thể nhóm chúng chung trong một object có chứa các thuộc tính lần lượt là chiều dài và chiều rộng của hình chữ nhật.

Tất cả các object đều có thể thay đổi trong khi chương trình đang chạy. Các thuộc tính và phương thức có thể được thêm vào object ngay khi nó được khai báo như là một const. Trong thực tế, một object được sử dụng để biểu diễn một thực thế cụ thể như con người, hóa đơn,... . Các thuộc tính được biểu diễn dưới dạng cặp bao gồm key (tên của thuộc tính) và value. Ví dụ sau đây cho thấy cách tạo ra một object đơn giản:
{% highlight js linenos %}
var emptyObject = {};
var person = {
    "firstname": "Long",
    "middlename": "Truong",
    "lastname": "Nguyen"
};
var person = {fullname: "NguyenTruongLong"};
{% endhighlight%}
Trong câu lệnh khai báo đâu tiên, chúng ta tạo ra một đối tượng không có bất kỳ thuộc tính và phương thức nào, đó là một đối tượng rỗng. Trong câu lệnh khai báo thứ hai, chúng ta tạo ba cặp chuỗi được ngăn cách với nhau bằng đấu phẩy đặt trong dấu ngoặc ngọn. Chuỗi đầu tiên trong mỗi cặp biểu diễn tên của thuộc tính trong khi chuỗi thứ hai trong mỗi cặp chuỗi biểu diễn giá trị của thuộc tính tương ứng với nó. Trong câu lệnh khai báo thứ ba chúng ta thấy rằng tên của thuộc tính là <em>fullname</em> cũng có thể không được đặt trong cặp dấu nháy. Tuy nhiên, trong các trường hợp sau đây, tên của thuộc tính bắt buộc phải được đặt trong cặp dấu nháy:
<ul>
 	<li>Tên của thuộc tính trùng với các <a href="http://www.javascripter.net/faq/reserved.htm" target="_blank" rel="noopener">từ khóa đặc biệt trong JavaScript</a></li>
 	<li>Tên của thuộc tính chứa các ký tự số</li>
 	<li>Tên của thuộc tính chứa bất kỳ ký tự đặc biệt nào khác ngoài các ký tự chữ cái, ký tự chữ số và ký tự $, hoặc ký tự _</li>
</ul>

{% highlight js linenos %}
{% raw %}
var o1 = {
    _ome$hing: 1,
    "111something": 0,
    "a or b or c": "a",
    "*%&amp;!@^#$^": true
};

var o2 = {
    1something: 1
};

var o3 = {
    a or b or c: "c"
};

var o4 = {
    *%&amp;!@^#$^: false
};
{% endraw %}
{% endhighlight%}

Trong 4 ví dụ trên, chỉ có object được khai báo của biến o1 là hợp lệ, còn 3 object từ các biến o2, o3 và o4 đều không hợp lệ do tên các thuộc tính trong các trường hợp đặc biệt không được đặt trong cặp dấu nháy.

Một object có thể chứa bất kỳ kiểu dữ liệu nào, bao gồm cả một object khác:
{% highlight js linenos %}
var book = {
    name: 'Catch-22',
    published: 1961,
    author: {
        firstname: 'Joseph',
        lastname: 'Heller'
    }
};
{% endhighlight%}
<h4><b>THUỘC TÍNH (PROPERTIES)</b></h4>
Có hai cách để truy cập thuộc tính của một object:
<ul>
 	<li>Gọi thông qua ký tự dấu chấm, ví dụ như hero.occupation</li>
 	<li>Gọi thông qua cặp dấu ngoặc vuông, ví dụ như hero['occupation']</li>
</ul>
Để thêm các thuộc tính của một object đã tồn tại ta hãy xem ví dụ sau:
{% highlight js linenos %}
hero.breed = 'turtle';
hero.name = 'Leonardo';
hero.sayName = function () {
    return hero.name;
};
{% endhighlight%}
Khi muốn xóa thuộc tính của một object, ta chỉ thực hiện đơn giản như sau:
{% highlight js linenos %}
var hero = {
    breed: 'Turtle',
    occupation: 'Ninja',
    say: function () {
        return 'I am ' + hero.occupation;
    }
};
delete hero.occupation;
hero.say();
hero['say']();
{% endhighlight%}
Để kiểm tra một thuộc tính của object có tồn tại hay không, chúng ta sử dụng hàm hasOwnProperty như sau:
{% highlight js linenos %}
superman.hasOwnProperty('city');
{% endhighlight%}
Nếu chúng ta truy cập một thuộc tính không tồn tại, giá trị undefined sẽ được trả về.
<h5><strong>GLOBAL OBJECT</strong></h5>
<h4><b>PHƯƠNG THỨC (METHODS)</b></h4>
Một thuộc tính trong object có thể trỏ đến một function. Các thuộc tính mà trỏ tới function thì cũng được gọi là các phương thức. Các phương thức biểu diễn các hành động mà một object có thể thực hiện. Hãy xem ví dụ sau đây:
{% highlight js linenos %}
var dog = {
    name: 'Benji',
    talk: function () {
        alert('Woof, woof!');
    }
};
{% endhighlight%}
Chúng ta có thể gán trực tiếp một anonymous function cho một thuộc tính như ví dụ sau đây:
{% highlight js linenos %}
person.fullname = function () {
    return "John Smith";
}
{% endhighlight%}
Chúng ta truy cập một phương thức của object cũng tương tự như truy cập thuộc tính, đó là sử dụng dấu chấm hoặc sử dụng cặp dấu ngoặc vuông:
{% highlight js linenos %}
var hero = {
    breed: 'Turtle',
    occupation: 'Ninja',
    say: function () {
        return 'I am ' + hero.occupation;
    }
};
hero.say();
hero['say']();
{% endhighlight%}
