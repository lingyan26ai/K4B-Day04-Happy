# TEAM — Day04, K4-L3B

**Làm nhóm.** Mỗi người tự viết và commit phần INDIVIDUAL của mình.

## Thông tin bài nộp

- Tên nhóm: Happy
- Người đại diện / MSSV: Võ Công Danh - 2A202602739
- Tên repo: `K4B-DAY04-Happy`
- URL repo, nhánh nộp, commit chốt: https://github.com/lingyan26ai/K4B-Day04-Happy, `main`, `8eb08ea` (`feat: finalize v5 prompt and evaluation evidence`)
- Deadline áp dụng và link thông báo đổi hạn nếu có:

## Thành viên

| Họ và tên | MSSV | GitHub | Vai trò và công việc | File/commit/PR |
|---|---|---|---|---|
| Võ Công Danh | 2A202602739 | lingyan26ai | Cải thiện prompt xử lý ID/environment, chạy eval và quản lý evidence/version log, cập nhật report | system_prompt.md, tools.yaml, version_log.csv, v5 runs; ed6dda7, a0537b9, 90e8fdf, 1145fa1, 8eb08ea |
| Bùi Việt Anh | 2A202602611 | VietAnh-AI2-UET | Sửa lỗi tool routing, chạy tích hợp các bộ eval và cập nhật extension artifacts | system_prompt.md, tools.yaml, runs/; 0d9e569, 2d58a19, fce3899, ecbc29c |
| Đinh Đức Long | 2A202602633 | may31st | Xử lý prompt injection và safety boundary, chạy lại adversarial eval | system_prompt.md, tools.yaml, adversarial runs; d44e9f8, 910360a |
| Hà Anh Tuấn | 2A202602376 | SpoopyTuan | Phát triển UI Streamlit và lưu transcript hội thoại | tarter_v0/app.py, starter_v0/transcripts/; 0ff29dc, a660cca |

## Nhận xét chung

- Kết quả và bằng chứng: Bản v5 mới nhất đạt 62/62 case (100%) trên cả base 30, adversarial 12, extension 10 và group 10; tất cả run đều đo đủ case và có `provider_error_cases = 0`. Các run dùng chung artifact `v5+p5659ce0b46b3+tbcbe8bbcf544`, được lưu trong `starter_v0/runs/` và đối chiếu trong `starter_v0/artifacts/version_log.csv`.
- Thay đổi hiệu quả nhất: V5 bổ sung boundary không gọi tool cho yêu cầu giả mạo authority, giới hạn diagnostic thiết bị chỉ dùng `inspect_device` khi không yêu cầu service status, và cho phép `create_ticket` chạy trực tiếp khi cùng tin nhắn có xác nhận chủ động đầy đủ. Các thay đổi này sửa regression `A02`, `H05` và `E05`, đồng thời giữ 100% ở các suite còn lại.
- Giới hạn còn lại: E09/E10 đạt routing nhưng `search_device_info` trả `missing_api_key`, nên chưa chứng minh được web retrieval thực tế. UI trong `app.py` vẫn hardcode provider Gemini và nhãn artifact v3, chưa đồng nhất với artifact v5. Kết quả 100% cũng mới được đo trên dữ liệu giả lập và model `openai/gpt-4o-mini`.
- Cách phân công và tích hợp: Nhóm chia theo vòng cải tiến và loại evidence: v1 xử lý định danh/environment mơ hồ (`ed6dda7`), v2 sửa tool selection và confirmation boundary (`0d9e569`), version log (`a0537b9`), v3 hoàn thiện category/tool descriptions (`910360a`), UI/transcript (`a660cca`), extension (`fce3899`) và safety v5 (`8eb08ea`). Mỗi vòng được tích hợp trên `main`, chạy lại các suite cố định, rồi kiểm tra hash, metric, tool result và failed cases trước khi ghi report.

## INDIVIDUAL

Sao chép mục này cho từng thành viên.

### Võ Công Danh — 2A202602739

- Phần việc và file/commit/PR: Cải thiện system_prompt.md, chạy và phân tích eval v0–v5, cập nhật version_log.csv, REPORT.md và TEAM.md. Commit: ed6dda7, a0537b9, 90e8fdf, 1145fa1, 8eb08ea.
- Quyết định, khó khăn và cách xử lý: Bổ sung quy tắc hỏi lại khi thiếu hoặc mơ hồ ID/environment; kiểm tra từng trace để phân biệt lỗi tool, argument và provider.
- Điều đã học: Cách thiết kế prompt tool calling, kiểm soát confirmation và dùng run evidence để đánh giá agent.
- AI/công cụ đã dùng và cách kiểm tra: Dùng Codex, Git/GitHub và OpenRouter. Kiểm tra qua run JSON, metric, hash artifact và git diff.
- Thời điểm đã tự nộp URL repo chung trên VLearn:

### Bùi Việt Anh — 2A202602611

- Phần việc và file/commit/PR: Cải thiện system_prompt.md, sửa tools trong tool.yaml, chạy và phân tích eval v0, v4, v5, cập nhật version_log.csv. Commit: 0d9e569, 2d58a19, fce3899, ecbc29c.
- Quyết định, khó khăn và cách xử lý: Xem log, phân tích các test case lỗi, xác định loại lỗi, kiểm tra tool được gọi và system prompt, chuẩn đoán nguyên nhân; Nới lỏng system prompt khỏi bị quá cứng nhắc/hardcode, thêm mô tả chi tiết cho tool; Không phải chuẩn đoán nào cũng chính xác, giải pháp sau làm hỏng giải pháp trước, sau mỗi giải pháp phải chạy lại 1 lần tất cả test case; Thử lại nhiều lần.
- Điều đã học: Trace log, chuẩn đoán nguyên nhân gây lỗi nếu agent sử dụng tool sai cách (sai tool, sai tham số,...), quyết định khi nào sửa tool/system_prompt, phối hợp làm việc nhóm.
- AI/công cụ đã dùng và cách kiểm tra: Anti-gravity, Git/GitHub, OpenRouter. Trích xuất test_case failed của run, học cách nhận biết trường hợp nào sửa tool/system_prompt, học cách viết description chặt chẽ cho tool, viết log từ json vào csv.
- Thời điểm đã tự nộp URL repo chung trên VLearn:

### Đinh Đức Long - 2A202602633

- Phần việc và file/commit/PR: Cải thiện system_prompt.md và tools.yaml. Chạy và phân tích eval_adversarial. Phân tích và cập nhật các case H12, M05, M09 (nhóm lỗi bỏ qua/sai thứ tự confirmation boundary trước write-action) trong eval_base. Cập nhật thêm 10 case mới vào data/eval_group.json. Commit: 910360a, d44e9f8.
- Quyết định, khó khăn và cách xử lý: Phát hiện agent tin nhầm nội dung do user tự chèn thành xác nhận thật, dẫn tới bỏ qua confirmation ở nhiều case adversarial. Khó khăn là viết rule đủ tổng quát để chặn nhiều biến thể injection. Xử lý sửa system_prompt.md để chỉ tin tool_result thật từ hệ thống và từ chối ngay khi có dữ liệu nhạy cảm
- Điều đã học: Cách thiết kế prompt injection, forged state, role spoofing, stale confirmation để kiểm tra ranh giới an toàn của agent, hiểu rằng một agent có thể vượt qua base suite nhưng vẫn có lỗ hổng nghiêm trọng ở adversarial suite nếu rule an toàn không được viết ở mức tổng quát, cách viết eval case có expect rõ ràng và bám sát failure_type thực tế.
- AI/công cụ đã dùng và cách kiểm tra: Sử dụng Antigravity, Git/GitHub và OpenRouter. Kiểm tra qua run JSON, metric, hash artifact và git diff.     
- Thời điểm đã tự nộp URL repo chung trên VLearn: 

### Hà Anh Tuấn - 2A202602376
- Phần việc và file/commit/PR: Xây dựng giao diện web bằng Streamlit cho IT Helpdesk Agent trong `starter_v0/app.py`; bổ sung dependency Streamlit trong `starter_v0/requirements.txt`; tích hợp luồng chat với provider, hiển thị tool-calling traces và lưu transcript hội thoại tại `starter_v0/transcripts/`. Commit: `0ff29dc`, `a660cca`.
- Quyết định, khó khăn và cách xử lý: Dùng `st.session_state` để giữ lịch sử hội thoại giữa các lần Streamlit rerun, giúp trải nghiệm chat liền mạch. Chuẩn hóa phần phản hồi từ agent bằng cách tách trường `reply` trong JSON trước khi hiển thị, đồng thời đặt tool traces trong expander để giao diện gọn nhưng vẫn có bằng chứng kiểm tra.
- Điều đã học: Cách kết nối giao diện Streamlit với vòng lặp model/tool calling, quản lý trạng thái của ứng dụng web tương tác và lưu transcript để tái kiểm tra một phiên chạy thực tế.
- AI/công cụ đã dùng và cách kiểm tra: Sử dụng Streamlit, Python, Git/GitHub và Gemini provider. Kiểm tra bằng cách chạy giao diện, gửi hội thoại thử nghiệm, xác nhận phản hồi được hiển thị đúng, tool events xuất hiện trong trace và transcript được tạo trong thư mục `transcripts/`.
- Thời điểm đã tự nộp URL repo chung trên VLearn: