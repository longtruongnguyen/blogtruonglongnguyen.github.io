---
layout: post
title: Thuật toán sắp xếp Merge Sort
keywords: "thuật toán sắp xếp merge sort, merge sort, thuật toán merge sort"
---

Merge Sort là thuật toán sắp xếp dựa trên chiến lược Chia để trị (Divide and Conquer) giống như Quicksort. Năm 1945, John von Neumann lần đầu tiên đề xuất ra thuật toán này.

<h4><strong>Ý tưởng cơ bản của thuật toán:</strong></h4>
<ul>
 	<li>Nếu danh sách đầu vào chỉ gồm có một phần tử thì dừng lại và kết thúc</li>
 	<li>Nếu danh sách đầu vào có từ hai phần tử trở lên:
<ul>
 	<li>Chia một danh sách đầu vào thành hai nửa danh sách</li>
 	<li>Gọi đệ quy thủ tục để sắp xếp hai nửa danh sách này</li>
 	<li>Hợp nhất hai nửa danh sách đã được sắp xếp này thành một danh sách được sắp xếp có thứ tự mới</li>
</ul>
</li>
</ul>
Sau đây là một ví dụ minh họa cho quá trình sắp xếp của thuật toán Merge Sort.
<h4><strong>Cài đặt thuật toán bằng ngôn ngữ Python:</strong></h4>

{% highlight python linenos %}
def merge_sort(input_arr):
    print('Splitting ', input_arr)
    if len(input_arr) > 1:
        i = 0
        j = 0
        k = 0
        mid = len(input_arr) // 2   # chọn vị trí mốc để phân chia danh sách ban đầu thành 2 danh sách con
        left_sub_arr = input_arr[:mid]  #  tạo danh sách con bên trái
        right_sub_arr = input_arr[mid:] # tạo danh sách con bên phải
        merge_sort(left_sub_arr)    # gọi đệ quy để sắp xếp thứ tự danh sách con bên trái
        merge_sort(right_sub_arr)   # gọi dệ quy để sắp xếp thứ tự danh sách con bên phải

        while i < len(left_sub_arr) and j < len(right_sub_arr): # hợp nhất hai danh sách con đã được sắp xếp thành một danh sách mới được sắp xếp có thứ tự 
            if left_sub_arr[i] < right_sub_arr[j]:
                input_arr[k] = left_sub_arr[i]
                i = i + 1
            else:
                input_arr[k] = right_sub_arr[j]
                j = j + 1
            k = k + 1

        while i < len(left_sub_arr):
            input_arr[k] = left_sub_arr[i]
            i = i + 1
            k = k + 1

        while j < len(right_sub_arr):
            input_arr[k] = right_sub_arr[j]
            j = j + 1
            k = k + 1
    print('Merging ', input_arr)

input_arr = [8, 36, 17, 9, 24, 2, 5]
merge_sort(input_arr)
print(input_arr)
{% endhighlight %}

### Độ phức tạp tính toán của giải thuật Merge Sort
