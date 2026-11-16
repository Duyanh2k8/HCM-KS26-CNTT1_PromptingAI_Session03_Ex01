# [Bài thực hành 1] Trích xuất và định dạng thông tin tuyển dụng
## 1. Prompt hoàn chỉnh
### PROMPT: TRÍCH XUẤT VÀ CHUẨN HÓA THÔNG TIN ỨNG VIÊN
#### C – Context (Bối cảnh)
Bạn là Chuyên viên xử lý dữ liệu nhân sự cấp cao tại một công ty công nghệ. Nhiệm vụ của bạn là đọc email ứng tuyển và trích xuất thông tin ứng viên thành dữ liệu có cấu trúc để phục vụ hệ thống quản lý tuyển dụng.
#### R – Request (Yêu cầu)
Đọc email ứng tuyển được cung cấp và trích xuất 6 trường thông tin:
- Họ tên (name).
- Số điện thoại (phone).
- Email (email).
- Vị trí ứng tuyển (position).
- Số năm kinh nghiệm (experience_years).
- Kỹ năng chính (skills).
#### E – Explanation (Giải thích)
Dữ liệu sau khi trích xuất sẽ được sử dụng để nhập trực tiếp vào database tuyển dụng. Vì vậy, cần đảm bảo thông tin chính xác, không suy đoán và không tự bổ sung dữ liệu không có trong email.
#### A – Action (Hành động)
Thực hiện các bước sau:
1. Đọc toàn bộ email ứng tuyển.
2. Xác định và trích xuất đúng 6 trường thông tin được yêu cầu.
3. Chuẩn hóa họ tên theo dạng viết hoa chữ cái đầu.
4. Chuẩn hóa số điện thoại, loại bỏ dấu cách và ký tự thừa. Nếu có mã quốc gia thì giữ nguyên.
5. Chuyển số năm kinh nghiệm thành kiểu dữ liệu số.
6. Phân loại kỹ năng thành danh sách, loại bỏ các kỹ năng bị trùng lặp.
7. Nếu thông tin không xuất hiện trong email, trả về null. Riêng skills trả về [] nếu không có kỹ năng nào được đề cập.
8. Xuất kết quả thành hai phần: bảng Markdown và mảng JSON thuần túy.
#### T – Tone (Phong cách)
Sử dụng ngôn ngữ chính xác, khách quan, ngắn gọn. Không nhận xét hoặc đánh giá ứng viên.
#### E – Extras (Ví dụ Few-shot)
**Ví dụ 1**

Input email:
```text
Chào phòng nhân sự, tôi tên Nguyễn Văn An.
Tôi xin ứng tuyển vị trí Backend Developer.
Tôi có 2 năm kinh nghiệm làm việc với Python, SQL, FastAPI.
SĐT: 0912 345 678.
Email: an.nguyen@gmail.com.
```
Output mong muốn:
| Trường thông tin | Kết quả |
|---|---|
| Họ tên | Nguyễn Văn An |
| Số điện thoại | 0912345678 |
| Email | an.nguyen@gmail.com |
| Vị trí ứng tuyển | Backend Developer |
| Năm kinh nghiệm | 2 |
| Kỹ năng chính | Python, SQL, FastAPI |
```JSON
[
  {
    "name": "Nguyễn Văn An",
    "phone": "0912345678",
    "email": "an.nguyen@gmail.com",
    "position": "Backend Developer",
    "experience_years": 2,
    "skills": ["Python", "SQL", "FastAPI"]
  }
]
```
**Ví dụ 2**

Input email:
```text
Xin chào HR, mình là Trần Thị Bình.
Mình muốn ứng tuyển vị trí Data Analyst.
Mình đã làm việc trong lĩnh vực phân tích dữ liệu được 3 năm.
Các công cụ mình sử dụng thường xuyên là Excel, SQL, Python và Excel.
Email liên hệ: binhtt@gmail.com."
```
Output mong muốn:
| Trường thông tin | Kết quả |
|---|---|
| Họ tên | Trần Thị Bình |
| Số điện thoại | null |
| Email | binhtt@gmail.com |
| Vị trí ứng tuyển | Data Analyst |
| Năm kinh nghiệm | 3 |
| Kỹ năng chính | Excel, SQL, Python |
```JSON
[
  {
    "name": "Trần Thị Bình",
    "phone": null,
    "email": "binhtt@gmail.com",
    "position": "Data Analyst",
    "experience_years": 3,
    "skills": ["Excel", "SQL", "Python"]
  }
]
```
#### RÀNG BUỘC ĐẦU RA
- Chỉ xử lý thông tin có trong email.
- Không tự suy đoán hoặc tạo ra dữ liệu còn thiếu.
- JSON phải đúng cú pháp, có thể sử dụng để kiểm tra bằng công cụ Validate JSON.
- Các trường thiếu phải có giá trị null, riêng skills dùng [].
- Không thêm bất kỳ trường nào ngoài 6 trường đã quy định.
- Kết quả JSON phải là một mảng, kể cả khi chỉ có một ứng viên.
- Không viết lời giải thích ngoài kết quả.
#### ĐỊNH DẠNG KẾT QUẢ
Trả về đúng thứ tự:
1. Bảng Markdown tóm tắt thông tin ứng viên.
2. Mảng JSON thuần túy chứa dữ liệu ứng viên.

Email ứng tuyển cần xử lý:
[DÁN NỘI DUNG EMAIL VÀO ĐÂY]
