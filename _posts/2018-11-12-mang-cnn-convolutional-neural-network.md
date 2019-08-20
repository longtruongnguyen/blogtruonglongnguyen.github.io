\subsection{Convolutional Neural Network}
Convolutional Neural Network (CNN) khá giống một mạng neural thông thường, bao gồm các nơ-ron có khả năng tự tối ưu hóa bằng quá trình học. Tuy nhiên, CNN được sử dụng chủ yếu trong việc xử lý ảnh, vì nếu sử dụng mạng nơ-ron thông thường sẽ cần rất nhiều trọng số (một hình kích thước 28x28x1 cần 784 trọng số). Vì vậy, các lớp trong CNN có nơ-ron được sắp xếp theo 3 chiều: width, height, depth. Ngoài ra, các nơ-ron trong một lớp chỉ liên kết với 1 vùng nhỏ trong lớp trước nó. Trong xử lý ngôn ngữ tự nhiên, ta có thể thay hình ảnh bằng một ma trận, mỗi hàng của ma trận là một vector đại diện một từ trong câu.

Lấy ví dụ, câu đầu vào được chuyển thành một ma trận $d \times k$ với $d$ là độ dài vector đại diện từ và $k$ là một số cố định quyết định chiều dài tối đa của câu. Ta chèn số 0 (zero-pad) cho ma trận câu để đạt được chiều dài $k$, nếu câu có chiều dài ngắn hơn. Với những câu có chiều dài lớn hơn $k$, ta có thể bỏ hoặc cắt ra thành các câu nhỏ hơn\cite{Lamb2015ConvolutionalEF}.   

Đây là kiến trúc của một bộ mã hóa CNN:
\begin{figure}[ht]
	\centering
	\includegraphics[scale=0.5]{images/CNNEncoder}
	\caption{Kiến trúc của bộ mã hóa CNN\cite{CNNEncoder}.}
	\label{HinhCNNKT}
\end{figure}

Tiếp theo, sẽ giới thiệu về các lớp của CNN: Convolution Layer, Pooling Layer và Non-linear Layer. 
\paragraph*{Convolution Layer}\mbox{}

Trong Convolution Layer, ta có $n$ filter (bộ lọc) $W$ được dùng để xác định các đặc trưng (feature) trên mảng dữ liệu $X$, ta sử dụng tích chập (convolution) trên mảng dữ liệu $X$ và các filter $W$ cho việc này. Quá trình tích chập được minh họa qua hình (\ref{HinhCNNSlide}).

\begin{figure}[ht]
	\centering
	\includegraphics[scale=0.3]{images/CNNSlide}
	\caption{Một ví dụ tích chập 2D qua 2 lần trượt Filter quanh mảng Data. Tại mỗi lần trượt Filter, đối với mảng Data màu xanh trùng với Filter, ta sẽ nhân từng giá trị phần tử trong mảng Data đó với giá trị phần tử có vị trí tương ứng trong Filter, sau đó tổng các số lại. Kết quả là giá trị một phần tử màu xanh tương ứng của mảng Convolved Feature.}
	\label{HinhCNNSlide}
\end{figure}

Để thực hiện tích chập, ta trượt (slide) từng $W$ quanh toàn bộ $X$ và tại mỗi lần trượt, ta nhân từng giá trị phần tử trong vùng mà $X$ khớp $W$ với giá trị phần tử có vị trí tương ứng trong $W$, sau đó tổng các số lại. Kết quả là giá trị một phần tử của mảng feature map $Y$. Với $n$ filter, ta có được $n$ feature map $Y$.

Ngoài ra, ta còn có 2 tham số ảnh hưởng đến quá trình tích chập: \textbf{stride} và \textbf{zero-padding}. Stride $S$ quyết định đơn vị di chuyển cho từng lần trượt. Với ví dụ trong hình (\ref{HinhCNNSlide}), stride = 1. Nếu stride = 2 thì với mỗi lần trượt, Filter sẽ di chuyển qua 2 cột hoặc 2 hàng trên Data. Zero-padding $Z$ quyết định số lần đệm thêm số 0 bao quanh toàn bộ dữ liệu. 

Tóm lại, khi Convolution Layer nhận dữ liệu kích thước $Width_{1} \times Height_{1} \times Depth_{1}$, với $n$ filter kích thước $F \times F \times Depth_{1}$ và các tham số $S$ và $Z$, sẽ tạo đầu ra với kích thước $Width_{2} \times Height_{2} \times Depth_{2}$, kích thước này được tính như sau:
\begin{equation}
Width_{2} = (Width_{1} - F + 2Z)/S + 1
\end{equation}
\begin{equation}
Height_{2} = (Height_{1} - F + 2Z)/S + 1
\end{equation}
\begin{equation}
Depth_{2} = n
\end{equation}

\paragraph*{Pooling Layer}\mbox{}

Pooling Layer có nhiệm vụ làm giảm không gian của các feature map, từ đó làm giảm các tham số và độ phức tạp tính toán. Có nhiều cách thực hiện việc này, một cách thường dùng là Max Pooling. Max Pooling được minh họa qua hình (\ref{HinhCNNMaxPool}).

\begin{figure}[ht]
	\centering
	\includegraphics[scale=0.5]{images/maxpool}
	\caption{Ví dụ về Max Pooling\cite{CNNMaxPool}. Hàm max được xét trên 1 vùng 2x2 và mỗi lần di chuyển có stride = 2.}
	\label{HinhCNNMaxPool}
\end{figure}

Với Max Pooling, ta tìm số lớn nhất trong một vùng nhất định trên feature map, kết quả sẽ là một phần tử trong feature map mới. Mỗi lần di chuyển tới vùng mới, ta di chuyển theo stride tương ứng.

Tóm lại, khi Pooling Layer nhận tập feature map kích thước $Width_{2} \times Height_{2} \times Depth_{2}$, với vùng để xét có kích thước $F' \times F'$ và tham số $S'$, sẽ tạo tập feature map mới với kích thước $Width_{3} \times Height_{3} \times Depth_{3}$, kích thước này được tính như sau:
\begin{equation}
Width_{3} = (Width_{2} - F')/S' + 1
\end{equation}
\begin{equation}
Height_{3} = (Height_{2} - F')/S' + 1
\end{equation}
\begin{equation}
Depth_{3} = Depth_{2}
\end{equation}

\paragraph*{Non-linear Layer}\mbox{}

Cuối cùng, trong Non-linear Layer, ta áp dụng hàm phi tuyến lên từng phần tử của các activation map, hàm phi tuyến thường được chọn là ReLU. Từ đây, ta có thể thực hiện lại các lớp Convolution Layer, Pooling Layer và Non-linear Layer để thu nhỏ thêm không gian kết quả hoặc đưa vào một Fully-Connected network, là mạng neural truyền thẳng thông thường, để xây dựng kết quả đại diện cho đầu vào.
