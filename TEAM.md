# TEAM — Day04, K4-L3B

**Làm nhóm.** Mỗi người tự viết và commit phần INDIVIDUAL của mình.

## Thông tin bài nộp

- Tên nhóm: Happy
- Người đại diện / MSSV: Võ Công Danh - 2A202602739
- Tên repo: `K4B-DAY04-Happy`
- URL repo, nhánh nộp, commit chốt:
- Deadline áp dụng và link thông báo đổi hạn nếu có:

## Thành viên

| Họ và tên | MSSV | GitHub | Vai trò và công việc | File/commit/PR |
|---|---|---|---|---|
| Võ Công Danh | 2A202602739 | lingyan26ai | | |
| Bùi Việt Anh | 2A202602611 | VietAnh-AI2-UET | | |
| Đinh Đức Long | 2A202602633 | may31st | | |
| Hà Anh Tuấn | 2A202602376 | SpoopyTuan | | |

## Nhận xét chung

- Kết quả và bằng chứng: Độ chính xác trên bộ base 30 case tăng liên tục từ 0.70 ở v0 lên 0.80 ở v1, 0.90 ở v2 và 1.00 ở v3. Run v3 đo đủ 30/30 case, đạt 30/30 case và không có lỗi provider; bằng chứng nằm trong `starter_v0/runs/v3_B_base_openrouter_20260915T202915678114.json` và `starter_v0/artifacts/version_log.csv`.
- Thay đổi hiệu quả nhất: V3 bổ sung ánh xạ category cụ thể cho `search_kb`, bắt buộc hỏi lại khi thiếu asset ID và làm rõ mô tả của các tool `clarify`, `search_kb`, `create_ticket`. Thay đổi này sửa cả ba lỗi còn lại của v2 (`H03`, `H10`, `M06`) và nâng case accuracy từ 0.90 lên 1.00 mà không phát sinh regression.
- Giới hạn còn lại: Kết quả 1.00 hiện chỉ được chứng minh trên một lần chạy bộ base cố định với `openai/gpt-4o-mini`; chưa có run và phân tích đầy đủ cho 10 case nhóm, 12 case adversarial, UI và transcript. Kết quả cũng có thể dao động giữa các lần gọi model, nên cần chạy lại và review thủ công các boundary liên quan đến xác nhận, ghi dữ liệu và bảo mật.
- Cách phân công và tích hợp: Nhóm chia công việc theo từng vòng cải tiến và evidence: v1 xử lý định danh/environment mơ hồ (`ed6dda7`), v2 sửa lựa chọn tool và confirmation boundary (`0d9e569`), cập nhật run/version log (`a0537b9`), và v3 hoàn thiện category cùng tool descriptions (`910360a`). Mỗi thay đổi được tích hợp lên `main`, sau đó chạy lại cùng bộ base và đối chiếu hash, metric, failed cases trước khi chốt phiên bản tiếp theo.

## INDIVIDUAL

Sao chép mục này cho từng thành viên.

### Họ và tên — MSSV

- Phần việc và file/commit/PR:
- Quyết định, khó khăn và cách xử lý:
- Điều đã học:
- AI/công cụ đã dùng và cách kiểm tra:
- Thời điểm đã tự nộp URL repo chung trên VLearn:
