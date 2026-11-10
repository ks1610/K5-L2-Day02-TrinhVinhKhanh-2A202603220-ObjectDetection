# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.


## Định nghĩa lớp

| Lớp | Định nghĩa của bạn | Ví dụ/điểm phân biệt |
|---|---|---|
| `car` | Phương tiện ô tô chở người, thường có kích thước nhỏ hoặc trung bình, thiết kế chủ yếu để chở hành khách. | Sedan, hatchback, SUV, coupe. Phân biệt với `van` dựa trên hình dáng thân xe và mục đích sử dụng. |
| `truck` | Phương tiện vận tải hàng hóa, thường có cabin riêng và thùng hoặc khoang chở hàng phía sau. | Xe tải thùng, xe tải mui bạt, xe tải ben. Không nhầm với xe van có khoang hàng liền thân. |
| `bus` | Phương tiện giao thông được thiết kế để chở nhiều hành khách, thường có thân xe dài và nhiều cửa sổ. | Xe buýt nội thành, xe khách, xe buýt đường dài. |
| `van` | Phương tiện có thân xe dạng hộp, thường có khoang hành khách hoặc khoang hàng nối liền với cabin. | Minivan, cargo van, passenger van. Phân biệt với `car` dựa trên thiết kế thân xe cao và khoang xe rộng. |

## Quy tắc chung

- Box bám sát vật thể nghĩa là: `Bounding box phải bao quanh toàn bộ phần vật thể nhìn thấy được, không lấy thừa quá nhiều vùng nền và không cắt mất phần vật thể đang hiển thị.`

- Vật thể bị che khuất: `Vẫn gán nhãn nếu có đủ đặc điểm để xác định vật thể và class. Box chỉ bao quanh phần nhìn thấy được, không tự suy đoán phần bị che khuất.`

- Vật thể bị cắt bởi rìa ảnh: `Vẫn gán nhãn nếu phần còn lại đủ để nhận diện vật thể và xác định class. Box kéo sát đến rìa ảnh, không mở rộng ra ngoài khung hình.`

- Vật thể rất nhỏ/mơ hồ: `Chỉ gán nhãn khi có đủ thông tin để xác định vật thể và class. Nếu quá nhỏ, mờ hoặc không thể phân biệt đáng tin cậy giữa các class, cần đánh dấu để review thay vì tự đoán.`

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh | Tình huống | Quyết định cuối | Lý do theo schema |
| --- | --- | --- | --- |
| `drive_001` | xe ô tô bị lấp một phần sau cột điện | vẽ box cho phần nhìn thấy của xe, gán nhãn car | vật thể vẫn có thể được nhìn rõ đặc chưng của ô tô còn |
| `drive_005` | Xác định vật thể là truck hay van| gán nhãn truck | phương tiện có cabin riêng và chỏ hàng hóa |
| `drive_034` | xe ô tô bị lấp một phẩn bởi khung ảnh | vẽ box cho phần có thể nhìn thấy của xe, gán nhãn car | đặc diểm nhận dạng phần nhìn thấy của xe cho thấy xe là loại SUV |
