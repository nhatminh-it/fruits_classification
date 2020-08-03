# FRUITS CLASSIFICATION - PHÂN LOẠI TRÁI CÂY
### I. TÓM TẮT: Phân loại trái cây dựa trên hình ảnh sử dụng các kĩ thuật machine learning
#### 1. Bài toán: 
- *Sự tiến bộ trong kỹ thuật xử lý hình ảnh và tự động hóa trong lĩnh vực công nghiệp thúc đẩy việc sử dụng nó trong hầu hết các lĩnh vực. Trong đó, phân loại trái cây dựa trên hình ảnh của nó vẫn còn là một thách thức. Việc phân loại trái cây có thể được sử dụng để thực hiện quá trình săp xếp và phân loại trái cây giúp quản lý, bảo quản những loại trái cây một cách tốt nhất có thể (những phương pháp bảo quản khác nhau dựa trên từng loại trái cây). Phương pháp truyền thống để phân loại trái cây là phân loại một cách thủ công, tốn thời gian và luôn phải có sự hiện diện của con người.*
#### 2. Phương pháp giải quyết: 
- *Sử dụng Machine Learning để xây dựng model phân loại trái cây dựa trên hình ảnh. Từ đó, có thể giúp quá trình sắp xếp và phân loại trái cây trở thành một quá trình tự động gần như hoàn toàn.*
- *Input: Ảnh của một loại trái cây trên nền đơn giản (1 màu)*
- *Output: Tên của loại trái cây đó*
### II. DỮ LIỆU
#### 1. Cấu trúc thư mục dữ liệu - fruits_data
Có 10 loại trái cây bao gồm 2500 ảnh. Với 10 loại trái cây khác nhau có 10 thư mục trong fruits_data tương ứng với chúng, Vd: cachua lưu trữ ảnh của trái cà chua. Mỗi thư mục chứa 250 ảnh của loại trái cây ở mục đó.
#### 2. Thu thập dữ liệu
Bộ dữ liệu được sử dụng trong bài này bao gồm 2500 ảnh. Được thu thập bằng cách ra siêu thị Big C sử dụng smartphone chụp ảnh lần lượt từng trái của mỗi loại, trong khoảng thời gian 4 tiếng - một số loại trái cây được mua về phòng riêng để chụp.
#### 3. Thuộc tính bộ dữ liệu
- Tổng số hình ảnh: 2500 ảnh
- Số loại trái cây: 10 loại
- Ảnh của mỗi loại: 250 ảnh
- Size ảnh: Bộ data sẽ để nguyên size gốc khi chụp bằng điện thoại nhưng khi sử dụng sẽ chuyển về size 200x200 pixel
- Định dạng tên tệp: `<tên quả>_<chỉ số>.jpg` - Ví dụ: cachua_1.jpg
- Tỉ lệ train/test size: Có 3 tỉ lệ được sử dụng trong bài để đánh giá: 80/20, 75/25, 70/30.
### III. CÁC KĨ THUẬT XỬ LÍ DATA
- *Chúng mình xử dụng 2 phương pháp tách biệt để xử lí data và training model đó là dựa trên màu sắc và cạnh*
#### 1. Xử lí data dựa trên màu của bức ảnh
- Resize ảnh về size 200x200
- Đưa bức ảnh về 2 màu sử dụng thuật toán K-means
- Loại bỏ màu sáng hơn của bức ảnh (Màu sáng hơn là màu nền, nên loại bỏ)
- Chia nhỏ bức ảnh thành 25 section (40x40)
- Tính trung bình và độ lệch chuẩn cho cả bức ảnh và cho từng section 40x40
#### 2. Xử lí data bằng kĩ thuật tìm cạnh
- Resize ảnh về size 200x200
- Cách 1:
  - Chuyển ảnh thành màu xám.
  - Xử dụng thuật toán Canny để tìm cạnh
- Cách 2: 
  - Đưa bức ảnh về 2 màu sử dụng thuật toán K-means
  - Chuyển ảnh thành màu xám.
  - Xử dụng thuật toán Canny để tìm cạnh
### IV. CÁC MODEL XỬ DỤNG ĐỂ TRAIN 
#### 1. Random forests1
- Đây là phương pháp xây dựng một tập hợp rất nhiều cây quyết định và sử dụng phương pháp voting để đưa ra quyết định về biến target cần được dự báo. Một ví dụ về Random Forest như sau: 
  - Giả sử bạn muốn đi tham quan du lịch Anh và có sự cân nhắc cho việc tham quan thành phố nào như: Manchester, Liverpool hay Birmingham. Để trả lời câu hỏi này bạn sẽ cần tham khảo rất nhiều ý kiến từ bạn bè, blog du lịch, tour lữ hành … Mỗi một ý kiến tương ứng với một Decision Tree trả lời các câu hỏi như: thành phố này đẹp không, có được tham quan các sân vận động khi đến thăm không, số tiền bỏ ra là bao nhiêu, thời gian để tham quan thành phố là bao lâu… Sau đó bạn sẽ có một rừng các câu trả lời để quyết định xem mình sẽ đi tham quan thành phố nào. Random Forest hoạt động bằng cách đánh giá các Decision Tree sử dụng cách thức voting để đưa ra kết quả cuối cùng.
#### 2. SVC 
-
