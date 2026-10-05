# Bonus 4C và homework: flip_idx, mirrored validation, custom sigma

## Kết quả

- Model flip_idx giải phẫu: Pose mAP50-95 val gốc = 0.4573, val lật gương = 0.4388.
- Model flip_idx đồng nhất: Pose mAP50-95 val gốc = 0.4169, val lật gương = 0.2977.
- OKS trung bình với sigma đều = 0.7450; với sigma ước lượng theo keypoint = 0.5414.

## Nhận xét

Val gốc chỉ có hổ quay phải nên có thể che lỗi flip_idx: model vẫn học tốt hướng xuất hiện trong cả train và val. Val lật gương đưa vào hướng quay trái và đổi nhãn theo giải phẫu, nhờ đó mức tụt mAP giữa hai model phản ánh khả năng giữ đúng danh tính chân trái/phải. Tập val triển khai nên cân bằng hướng quay, gồm cặp ảnh gốc-lật, tư thế chân bắt chéo, occlusion và motion blur.

Sigma riêng được hiệu chỉnh từ median residual đã chuẩn hoá theo căn diện tích object và chặn trong [0.02, 0.25]. Đây là hiệu chỉnh thực nghiệm; với dataset thật nên dùng nhiều annotator độc lập và một calibration split riêng để tránh dùng val hai lần.
