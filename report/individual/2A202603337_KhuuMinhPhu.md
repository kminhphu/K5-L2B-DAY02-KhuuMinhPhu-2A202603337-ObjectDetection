# Báo cáo cá nhân — Ngày 2 Object Detection

Đổi tên file theo `MSSV_HoTen.md`, ví dụ `20241234_NguyenVanAn.md`. Điền kết quả thật, xóa dòng hướng dẫn khi nộp. Xem [quy định nộp](../../SUBMISSION.md).

## 1. Thông tin học viên

- Họ tên: Khưu Minh Phú
- MSSV: 2A202603337
- Email: phukhuu39@gmail.com
- Lớp: L2B
- Link repo bài làm: https://github.com/kminhphu/K5-L2B-DAY02-KhuuMinhPhu-2A202603337-ObjectDetection
- Link Colab đã chạy: https://colab.research.google.com/drive/1Bb-hi6CHJCfDDV2772Ygibf_Wz5pPowR?usp=sharing

## 2. Schema và mini guideline

Dẫn tới [GUIDELINE_MINI.md](../../GUIDELINE_MINI.md). Tóm tắt ba ca mơ hồ đã quyết định, cách áp dụng schema và phần cần giảng viên làm rõ.

## 3. Annotation và self-QC

- Số file nhãn train: 50
- Kết quả checker và lỗi đã xử lý: 3
- Danh sách ít nhất 10 ảnh đã rà bằng mắt: drive_001, drive_008, drive_010, drive_011, drive_013, drive_023, drive_025, drive_031, drive_032, drive_035, drive_038, drive_040, drive_043, drive_044, drive_049, drive_050
- Lỗi bỏ sót/box/class phát hiện khi rà và cách sửa: gán thêm nhãn
- Commit khóa nhãn ban đầu: 

## 4. Gold QC và rework

| Chỉ số | Trước sửa | Sau sửa nếu có |
|---|---:|---:|
| TP |375 | |
| FP |265 | |
| FN |278 | |
| Precision |0.5859 | |
| Recall |0.5743 | |
| F1 |0.58 | |
| mean_iou_of_matches |0.8726 | |
| passed |false | |

Dẫn tới `outputs/annotation_evaluation.json` trong repo. Nếu rework, ghi ảnh, lỗi đã kiểm, quyết định sửa/giữ và lý do. Không suy nguyên nhân chỉ từ FP/FN. Không có rework thì ghi rõ.

## 5. Kết quả YOLO

- Runtime, GPU/CPU, phiên bản Ultralytics và Torch: Runtime 2m16s, GPU/CPU: GPU T4, Ultralytics 8.4.208, Python-3.13.16, torch-2.14.1+cu130, CUDA:0, 
- Các tham số thay đổi so với notebook nếu có và lý do:
- Đường dẫn best checkpoint trong phiên chạy: best checkpoint: /content/Day2-Lab/outputs/yolo26_runs/vehicle_annotation/weights/best.pt

| Chỉ số trên 10 ảnh eval | Giá trị |
|---|---:|
| Precision |0.41010614003351986 |
| Recall |0.22981721226162247 |
| mAP50 |0.27193440295574317 |
| mAP50–95 |0.20155101272869613 |

Đặt cả 2 folder `assets/eval_predictions/` và `assets/yolo26_runs/` (giải nén từ `day2_colab_outputs.zip`) cạnh báo cáo và dẫn link tương đối. Không chỉ ghi số; chỉ ra ít nhất một ảnh và vật thể cụ thể.

Trả lời bốn câu hỏi cuối notebook:

1. Lớp nào recall thấp nhất? Ảnh nào minh họa?
Trả lời: Lớp bus có recall thấp nhất, ảnh minh họa là drive_058
2. Nếu mAP50 cao nhưng mAP50–95 thấp, cần kiểm điều gì trên box?
Trả lời: Kiểm tra Bounding Box và gán nhãn đã đúng chưa
3. Lỗi class nào có thể liên quan guideline? Dữ kiện nào hỗ trợ nhận xét? 
Trả lời: Class có hình dạng tương tự, có tỷ lệ nhầm lẫn cao. Dựa vào Precision thấp và Recall thấp và Guideline để nhận xét.
4. Vì sao không dùng 10 ảnh eval để train? Vai trò validation của chúng trong notebook là gì?
Trả lời: Không dùng 10 ảnh eval để train là để tránh tình trạng overfitting. Vai trò validation của chúng trong notebook là để chấm điểm mô hình sau mỗi vòng học xem độ chính xác đến đâu, giúp notebook tự động dừng lại khi thấy mô hình bắt đầu học quá đà và tự động lưu lại file trọng số tốt nhất.
## 6. Khó khăn và cách xử lý

| Bước/thời điểm | Lỗi quan sát | Cách đã thử | Kết quả/còn thiếu |
|---|---|---|---|
|Gán nhãn |Mơ hồ với bus hoặc car |Hỏi |Gán nhãn bus |
|Gán nhãn |Xe bị khuất |Đọc Guideline |Không gán nhãn |
## 7. Tự đánh giá theo rubric
| Tiêu chí | Kết quả bài làm | Điểm |
| --- | --- | ---: |
| Hoàn thành và định dạng YOLO | 50 file cùng basename, 5 cột, normalized, bốn class ID đúng | 10 |
| Đầy đủ vật thể | gán đủ xe thuộc schema, kể cả xe che/cắt khung có thể nhận diện | 20 |
| Độ bám sát và hình học box | box sát phần vật thể nhìn thấy, không lấn nền/gộp vật thể | 20 |
| Phân lớp nhất quán | phân biệt `car/truck/bus/van`, không gán vật thể ngoài scope | 15 |
| Mini guideline và quyết định mơ hồ | định nghĩa lớp, quy tắc box, ít nhất ba case có lý do | 10 |
| Gold-set annotation QC | `F1 = 0.58` và `mean IoU = 0.8726`| 5 |
| Pipeline YOLO và phân tích | Colab chạy được, không dùng eval để train, có metrics/ảnh eval và nhận xét lỗi | 10 |

Đối chiếu [RUBRIC.md](../../RUBRIC.md): phần nào đã có kết quả, phần nào còn thiếu hoặc chưa kiểm được. Không tự nhận hoàn thành bước chưa chạy.
## 8. Công cụ AI và tài liệu tham khảo
Gemini dùng ở bước gán nhãn để tìm hiểu về các loại xe.
Ghi công cụ đã dùng, dùng ở bước nào và phần đã tự kiểm tra; không dùng thì ghi rõ. Liệt kê nguồn ngoài repo được sử dụng. Không ghi mật khẩu/token hoặc đính kèm gold train.
