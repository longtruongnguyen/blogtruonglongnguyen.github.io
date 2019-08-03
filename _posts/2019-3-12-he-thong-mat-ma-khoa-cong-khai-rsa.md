---
layout: post
title: Hệ thống mật mã khóa công khai RSA
description: Hệ thống mật mã khóa công khai RSA được đặt tên dựa theo tên của những người phát minh ra nó là Ronald L. Rivest, Adi Shamir và Leonard M. Adleman.
keywords: "khóa công khai RSA, hệ thống mật mã RSA, mã hóa công khai RSA, mã hóa RSA, hệ thống mật mã khóa công khai RSA, khóa RSA"
---

RSA được đặt tên dựa theo tên của những người phát minh ra nó là Ronald L. Rivest, Adi Shamir và Leonard M. Adleman. Những người này đã tạo ra hệ thống mật mã khóa công khai RSA khi họ còn đang làm việc tại Viện Công nghệ Massachusetts (MIT). Trong phạm vi của bài viết này, mình sẽ trình bày về ý tưởng cơ chế hoạt động của hệ thống mật mã khóa công khai RSA, các cơ sở lý thuyết toán học trong quá trình mã hóa và giải mã thông điệp cùng với ví dụ minh họa cụ thể.

### Cơ chế hoạt động

Để mọi người có thể dễ hiểu hơn, mình sẽ dùng một ví dụ cụ thể sau đây để giải thích về cơ chế hoạt động của RSA. Giả sử Lan muốn gửi thư cho Điệp nhưng không muốn bị người khác có thể đọc được thư của mình.

### Cơ sở toán học

**_<span style="color:black">Rất dễ để thực hiện quá trình tìm một số nguyên tố ngẫu nhiên với kích thước cho trước</span>_**

**_<span style="color:black">Cho 2 số $$p$$ và $$q$$, quá trình tính tích $$n = pq$$ luôn được thực hiện dễ dàng</span>_**

**_<span style="color:black">Cho số $$n$$, quá trình tìm lại các thừa số nguyên tố $$p$$ và $$q$$ là rất khó</span>_**

**_<span style="color:black">Cho các số $$m$$, $$n$$ và $$e$$, quá trình tính $$c = {m^e}\,\bmod \,n$$ luôn được thực hiện dễ dàng</span>_**

**_<span style="color:black">Cho các số $$n, e, c$$ và các thừa số nguyên tố $$p$$ và $$q$$, quá trình tìm $$m$$ sao cho thỏa mãn $$c = {m^e}\,\bmod \,n$$ luôn được thực hiện dễ dàng</span>_**

**_<span style="color:black">Chỉ cung cấp các số $$n, e, c$$ nhưng không cung cấp các thừa số nguyên tố $$p$$ và $$q$$, quá trình tìm $$m$$ sao cho thỏa mãn $$c = {m^e}\,\bmod \,n$$ là không dễ dàng</span>_**

### Tạo cặp khóa trong RSA

Một cặp **Public Key** và **Private Key** trong RSA có thể được tạo thành thông qua các bước sau đây:

1. Tạo ra ngẫu nhiên một cặp số nguyên tố $p$ và $q$ có kích thước rất lớn
2. Tính $n$ với $$n = pq$$
3. Chọn ra một số mũ lẻ công khai (odd public exponent) $e$ có giá trị từ $3$ đến $n-1$ mà nguyên tố cùng nhau (coprime) với $p-1$ và $q-1$
4. Tính toán số mũ bí mật (private exponent) $d$ từ $e, p$ và $q$ với e thỏa mãn {% raw %}$$de \equiv 1\,\,\left( {\bmod \,L} \right)$${% endraw %}, trong đó {% raw %}$$L = LCM\left( {p - 1,q - 1} \right)$${% endraw %}
5. Gán $$public\,key = (n, e)$$ và $$private\,key = (n, d)$$

### Mã hóa nội dung trong RSA

Giả sử ta có một thông điệp $$m$$ cần được mã hóa thành ciphertext $$c$$ trước khi gửi đi, khi đó:
{% raw %}
$$\begin{align}
c = ENCRYPT\left( m \right) = {m^e}\bmod n
\end{align}$$
{% endraw %}

### Giải mã nội dung trong RSA
Khi người nhận cần giải mã thông điệp đã được mã hóa $$c$$ thành lại thông điệp gốc ban đầu $$m$$, hàm giải mã sẽ được thực hiện như sau:
{% raw %}
$$\begin{align}
m = DECRYPT\left( c \right) = {c^d}\bmod n
\end{align}$$
{% endraw %}
