# FRUITS CLASSIFICATION - PHÂN LOẠI TRÁI CÂY
### I. TÓM TẮT: Phân loại trái cây dựa trên hình ảnh sử dụng các kĩ thuật machine learning
#### 1. Bài toán: 
- *Sự tiến bộ trong kỹ thuật xử lý hình ảnh và tự động hóa trong lĩnh vực công nghiệp thúc đẩy việc sử dụng nó trong hầu hết các lĩnh vực. Trong đó, phân loại trái cây dựa trên hình ảnh của nó vẫn còn là một thách thức. Việc phân loại trái cây có thể được sử dụng để thực hiện quá trình săp xếp và phân loại trái cây giúp quản lý, bảo quản những loại trái cây một cách tốt nhất có thể (những phương pháp bảo quản khác nhau dựa trên từng loại trái cây). Phương pháp truyền thống để phân loại trái cây là phân loại một cách thủ công, tốn thời gian và luôn phải có sự hiện diện của con người.*
#### 2. Phương pháp giải quyết: 
- *Sử dụng Machine Learning để xây dựng model phân loại trái cây dựa trên hình ảnh. Từ đó, có thể giúp quá trình sắp xếp và phân loại trái cây trở thành một quá trình tự động gần như hoàn toàn.*
- *Input: Ảnh của một loại trái cây trên nền đơn giản (1 màu).*
- *Output: Tên của loại trái cây đó.*
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
- Tỉ lệ train/test size: 75/25
### III. CÁC KĨ THUẬT XỬ LÍ DATA
- *Chúng mình sử dụng 2 phương pháp tách biệt để xử lí data và training model đó là dựa trên màu sắc và cạnh. Sau đó kết hợp lại với nhau để train model.*
#### 1. Xử lí data dựa trên màu của bức ảnh
- Resize ảnh về size 200x200.
- Đưa bức ảnh về 2 màu sử dụng thuật toán K-means.
- Loại bỏ màu sáng hơn của bức ảnh (Màu sáng hơn thường là màu nền, nên loại bỏ).
- Chia nhỏ bức ảnh thành 25 section (40x40).
- Tính trung bình và độ lệch chuẩn cho:
    - Hướng thứ nhất: Ba chanel màu
    - Hướng thứ hai: Cho từng section 

<img src="https://i.imgur.com/iKcdC3k.png"><img src="https://i.imgur.com/UaKw9ZY.png">
<img src="https://i.imgur.com/jPHzXXh.png"><img src="https://i.imgur.com/QXKUhEC.png">
<img src="https://i.imgur.com/UM2I7CV.png"><img src="https://i.imgur.com/GtArom6.png">
<img src="https://i.imgur.com/iEf8cjY.png"><img src="https://i.imgur.com/nHLbRJV.png">
<img src="https://i.imgur.com/sRVs5Mi.png"><img src="https://i.imgur.com/1GQlA2j.png">

#### 2. Xử lí data bằng kĩ thuật tìm cạnh
- Resize ảnh về size 200x200.
- Hướng thứ nhất: 
  - Đưa bức ảnh về 2 màu sử dụng thuật toán K-means.
  - Xử dụng thuật toán Canny để tìm cạnh.
  - Chia nhỏ bức ảnh thành 25 section (40x40).
  - Tính trung bình và độ lệch chuẩn cho từng section.
- Hướng thứ hai:
  - Xử dụng thuật toán Canny để tìm cạnh.
  - Chia nhỏ bức ảnh thành 25 section (40x40).
  - Tính trung bình và độ lệch chuẩn cho từng section.
 
<img src="https://i.imgur.com/xwPDg30.png"><img src="https://i.imgur.com/n2nfmmd.png">
<img src="https://i.imgur.com/EpTKWqe.png"><img src="https://i.imgur.com/B2Dg2Tm.png">
<img src="https://i.imgur.com/XQMM0Qr.png"><img src="https://i.imgur.com/KooV5nv.png">
<img src="https://i.imgur.com/ghea90W.png"><img src="https://i.imgur.com/li8OxGy.png">
<img src="https://i.imgur.com/usETDBE.png"><img src="https://i.imgur.com/HD0iNku.png">

### IV. CÁC MODEL SỬ DỤNG ĐỂ TRAIN 
#### 1. Random Forest Classifier
- Đây là phương pháp xây dựng một tập hợp rất nhiều cây quyết định và sử dụng phương pháp voting để đưa ra quyết định về biến target cần được dự báo. 
- Tìm hiểu thêm về [Random Forest Classifier](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html?highlight=random%20forest#sklearn.ensemble.RandomForestClassifier)
#### 2. SVC - Support Vector Classification
- Áp dụng thuật toán dựa trên libsvm (thư viện svm). Thời gian tính toán ít nhất bằng bậc 2 của số lượng samples và có thể không thể áp dụng với số lượng samples vượt quá 10000
- Tìm hiểu thêm về [Support Vector Classification](https://scikit-learn.org/stable/modules/generated/sklearn.svm.SVC.html?highlight=svc#sklearn.svm.SVC)
### V. KẾT QUẢ ĐÁNH GIÁ
- Thực hiện các model machine learning đối với 4 hướng tiếp cận:
  - Sử dụng trung bình và độ lệch chuẩn cho từng lớp RGB của ảnh đã cluster: 
  
  <img src="https://i.imgur.com/PMEp04P.png">
  
  - Sử dụng trung bình và độ lệch chuẩn cho toàn ảnh đã được cluster về 2 màu với các section 40 x 40 pixels:
  
  <img src="https://i.imgur.com/vWKmf4j.png">
  
  - Sử dụng trung bình và độ lệch chuẩn của các giá trị pixels của từng section 40 x 40 với ảnh gốc được xử lý về canny edge:
  
  <img src="https://i.imgur.com/qKdPBTp.png">
  
  - Sử dụng trung bình và độ lệch chuẩn của các giá trị pixels của từng section 40 x 40 với ảnh đã được cluster chỉ còn 2 màu và được xử lý về canny edge:
  
  <img src="https://i.imgur.com/nyK4ES2.png">
  
### VI. KẾT LUẬN
- Sau khi đã có kết quả đánh giá sơ bộ, nhóm quyết định sử dụng kết hợp 2 trên 4 phương pháp ở trên:
    - Xử lí màu: Hướng thứ nhất
    - Xứ lí cạnh: Hướng thứ nhất 
- Kết quả:

<img src="https://i.imgur.com/mPrzEtp.png">

- Kết quả trên bộ valid data:

<img src="https://i.imgur.com/FOQ05xg.png">





