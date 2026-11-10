# Báo cáo cá nhân — Ngày 2 Object Detection

Đổi tên file theo `MSSV_HoTen.md`, ví dụ `20241234_NguyenVanAn.md`. Điền kết quả thật, xóa dòng hướng dẫn khi nộp. Xem [quy định nộp](../../SUBMISSION.md).

## 1. Thông tin học viên

- Họ tên: Trịnh Vinh Khánh
- MSSV: 2A202603220
- Email: trinhvinhkhanh1610@gmail.com
- Lớp: L2A
- Link repo bài làm: https://github.com/ks1610/K5-L2-Day02-TrinhVinhKhanh-2A202603220-ObjectDetection
- Link Colab đã chạy: https://colab.research.google.com/drive/1WHLHeQPQev6jesrrYcNL0SSBm7Ty52x0?usp=sharing

## 2. Schema và mini guideline

Dẫn tới [GUIDELINE_MINI.md](../../GUIDELINE_MINI.md). Tóm tắt ba ca mơ hồ đã quyết định, cách áp dụng schema và phần cần giảng viên làm rõ.

## 3. Annotation và self-QC

- Số file nhãn train: `50`
- Kết quả checker và lỗi đã xử lý: 
    ```
    - Các nhãn được gắn đúng với vâtj thể tuy nhiên có một số nhãn bị gán sai và thiếu
    - Lỗi sử lý: Gán sai nhãn bus và truck, van và car. Gán người trong ảnh thành van 
    ``` 
- Danh sách ít nhất 10 ảnh đã rà bằng mắt:
```
    - drive_001.jpg
    - drive_002.jpg
    - drive_003.jpg
    - drive_004.jpg
    - drive_005.jpg
    - drive_006.jpg
    - drive_007.jpg
    - drive_008.jpg
    - drive_009.jpg
    - drive_010.jpg
    - drive_011.jpg
    - drive_012.jpg
    - drive_013.jpg
    - drive_014.jpg
    - drive_015.jpg
    - drive_016.jpg
    - drive_017.jpg
    - drive_018.jpg
    - drive_019.jpg
    - drive_020.jpg
    - drive_021.jpg
    - drive_022.jpg
    - drive_023.jpg
    - drive_024.jpg
    - drive_025.jpg
    - drive_026.jpg
    - drive_027.jpg
    - drive_028.jpg
    - drive_029.jpg
    - drive_030.jpg
    - drive_031.jpg
    - drive_032.jpg
    - drive_033.jpg
    - drive_034.jpg
    - drive_035.jpg
    - drive_036.jpg
    - drive_037.jpg
    - drive_038.jpg
    - drive_039.jpg
    - drive_040.jpg
    - drive_041.jpg
    - drive_042.jpg
    - drive_043.jpg
    - drive_044.jpg
    - drive_045.jpg
    - drive_046.jpg
    - drive_047.jpg
    - drive_048.jpg
    - drive_049.jpg
    - drive_050.jpg
```
- Lỗi bỏ sót/box/class phát hiện khi rà và cách sửa:
```
Lỗi bỏ sót với nhãn van.
Cách khắc phục: Gán nhãn tay cho vật thể.
```
- Commit khóa nhãn ban đầu: `10c79199b4588f9c43901282afa61bee1e1a59e2`

## 4. Gold QC và rework

| Chỉ số | Trước sửa | Sau sửa |
|---|---:|---:|
| TP | 371 |  |
| FP | 304 |  |
| FN | 282 |  |
| Precision | 0.5496 |  |
| Recall | 0.5681 |  |
| F1 | 0.5587 |  |
| mean_iou_of_matches | 0.8343 |  |
| passed | false |  |

Dẫn tới `outputs/annotation_evaluation.json` trong repo. Nếu rework, ghi ảnh, lỗi đã kiểm, quyết định sửa/giữ và lý do. Không suy nguyên nhân chỉ từ FP/FN. Không có rework thì ghi rõ.

## 5. Kết quả YOLO

- Runtime, GPU/CPU, phiên bản Ultralytics và Torch:
`cpu: CPU (Intel Xeon CPU @ 2.20GHz), Ultralytics 8.4.208,
torch-2.14.1`
- Các tham số thay đổi so với notebook nếu có và lý do: `không có`
- Đường dẫn best checkpoint trong phiên chạy:
`"checkpoint": "/content/K5-L2-Day02-TrinhVinhKhanh-2A202603220-ObjectDetection/outputs/yolo26_runs/vehicle_annotation/weights/best.pt"`

| Chỉ số trên 10 ảnh eval | Giá trị |
|---|---:|
| Precision | 0.4630518544584381 |
| Recall | 0.23306737588652485 |
| mAP50 | 0.274593521666665 |
| mAP50–95 | 0.20350889173117306 |

Đặt cả 2 folder `assets/eval_predictions/` và `assets/yolo26_runs/` (giải nén từ `day2_colab_outputs.zip`) cạnh báo cáo và dẫn link tương đối. Không chỉ ghi số; chỉ ra ít nhất một ảnh và vật thể cụ thể.

Trả lời bốn câu hỏi cuối notebook:

1. Lớp nào recall thấp nhất? Ảnh nào minh họa?
```
Class bus và van là hai lớp có Recall thấp nhất
bus: Recall = 0.000 (0%)
van: Recall = 0.0833 (8.33%)

Ảnh minh họa: 
- drive_051.jpg: nhãn van đè lên nhãn car
- drive_052.jpg: mô hình nhận diện nhầm thènh 2 bus trong khi chỉ có 1
```
2. Nếu mAP50 cao nhưng mAP50–95 thấp, cần kiểm điều gì trên box?

```
Cần kiểm tra:
- Vị trí Bounding box có bị lệch so với vật thể  không
- Kích thước Box có quá rộng hoặc quá hẹp so với vật thể không
- Biên Box có bao phủ chính xác toàn bộ vật thể không
- Ground Truth Bounding box được gán nhãn có nhất quán và chính xác không
```
3. Lỗi class nào có thể liên quan guideline? Dữ kiện nào hỗ trợ nhận xét?
```
Class giữa car và van.
Dữ kiện từ ảnh:
- drive_051.jpg: Chiếc xe màu đỏ ở phía dưới ảnh được dự đoán là van 0.96, mặc dù hình dáng bên ngoài khá giống một chiếc ô tô con.
- drive_054.jpg: Chiếc xe màu đỏ ở bên phải cũng được dự đoán là van 0.95. 
Điều này đặt ra khả năng guideline phân biệt car và van chưa đủ rõ ràng.
```
4. Vì sao không dùng 10 ảnh eval để train? Vai trò validation của chúng trong notebook là gì?
```
Nếu sử dụng những ảnh này để huấn luyện, mô hình có thể ghi nhớ đặc điểm của chúng thay vì thực sự học được khả năng tổng quát hóa trên dữ liệu mới.

Vai trò của dữ liệu validation/evaluation:
- Kiểm tra khả năng phát hiện vật thể trên dữ liệu chưa được sử dụng để cập nhật trọng số.
- Theo dõi các chỉ số Precision, Recall, mAP50 và mAP50–95.
- Phát hiện các vấn đề như bỏ sót vật thể, dự đoán sai class và bounding box không chính xác.
- Hỗ trợ đánh giá và lựa chọn cấu hình mô hình phù hợp.
```

## 6. Khó khăn và cách xử lý

| Bước/thời điểm | Lỗi quan sát | Cách đã thử | Kết quả/còn thiếu |
|---|---|---|---|
| CP2 — Gán nhãn | Các vật thể đè lên nhau | kéo box cho các phần có thể nhìn thấy mỗi vật | có thể đảm bảo bao phủ gần đủ cho một vật thể nhưng vật còn lại bị khuất một phần |

## 7. Tự đánh giá theo rubric

Đối chiếu [RUBRIC.md](../../RUBRIC.md): phần nào đã có kết quả, phần nào còn thiếu hoặc chưa kiểm được. Không tự nhận hoàn thành bước chưa chạy.

```
Đánh giá theo RUBRIC.md:
- Các tiêu chỉ đã hoàn thành:
[v]Hoàn thành và định dạng YOLO
[v]Đầy đủ vật thể
[v]Độ bám sát và hình học box
[v]Phân lớp nhất quán
[v]Mini guideline và quyết định mơ hồ
[v]Pipeline YOLO và phân tích

Theo Lab Coach, tập gold_train_labels đang gặp lỗi gắn nhầm nhãn nên chưa thể đối chiếu ở phần Gold-set annotation QC
```
## 8. Công cụ AI và tài liệu tham khảo

Ghi công cụ đã dùng, dùng ở bước nào và phần đã tự kiểm tra; không dùng thì ghi rõ. Liệt kê nguồn ngoài repo được sử dụng. Không ghi mật khẩu/token hoặc đính kèm gold train.
```
- Công cụ sử dụng: nuctl (Nuclio Command-Line Interface / nuctl CLI)
- Bước dử dụng: CP2 — Gán nhãn

Công cụ hỗ  trợ gán nhãn tự động cho 4 nhãn, tuy nhiên sau khi dùng công cụ, vẫn cần duyệt thủ công toàn bộ 50 ảnh đến điều chỉnh box và gán nhãn còn thiếu 
```
