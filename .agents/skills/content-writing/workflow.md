# Quy trình chi tiết soạn nội dung

1. **Thu thập thông tin**
   - Nghiên cứu đề tài, phân tích đối thủ, lắng nghe phản hồi khách hàng.
   - Ghi chú các ý quan trọng, số liệu, trích dẫn.
2. **Lập dàn ý**
   - Xác định các ý chính.
   - Đối với bài dài, phân chia thành các phần phụ (H2/H3).
3. **Triển khai nội dung dựa vào dàn ý**
4. **Kiểm tra logic và luồng**
   - Rà soát xem ý chuyển tiếp mượt mà chưa.
   - Thứ tự có hợp lí với hành trình độc giả?
5. **Sửa ngôn ngữ**
   - Chuyển từ ngữ phức tạp sang đời thường.
   - Rút gọn câu, đảm bảo dễ đọc trên web (đối với blog).
6. **Hoàn thiện & kiểm tra cuối cùng**
   - Chạy kiểm tra chính tả, ngữ pháp.
   - Đặt CTA rõ ràng: đọc tiếp, đăng ký, mua hàng…
7. **Xuất bản & theo dõi**
   - Gắn thẻ, meta (nếu trên blog).
   - Theo dõi tương tác, chuẩn bị tối ưu trong lần sau.

**⚠️ Quy tắc:** Sau mỗi bước hoàn thành, AI Agent dừng lại chờ xác nhận từ bạn trước khi tiếp tục bước tiếp theo.

## Cấu trúc folder & file cho từng bài

- Mỗi bài viết là **1 folder riêng**, đặt tên theo mẫu: `id-slug`.
- Ví dụ: `1-full-stack-chuan-ky-su`.
- Loại nội dung (script video ngắn, script video dài, post, blog) được ghi trong file `00-brief.md`.

```text
content-writing/
   du-an/
      1-full-stack-chuan-ky-su/
         00-brief.md
         01-thu-thap-thong-tin.md
         02-dan-y.md
         03-noi-dung-chinh-thuc.md
```

### Mẫu ghi chú trong `00-brief.md`

```text
ID: 1
Slug: full-stack-chuan-ky-su
Loai-noi-dung: script-video-ngan
Muc-tieu: ...
Doi-tuong: ...
```

### Quy ước trạng thái file

Mỗi file nội dung (dàn ý, script, bài viết) **bắt buộc** phải có trường `Trang-thai` ở đầu file để theo dõi tiến độ giữa các phiên làm việc.

**Các giá trị hợp lệ:**
- `cho-duyet` — Nội dung đã hoàn thành, đang chờ người dùng xác nhận/duyệt.
- `da-duyet` — Người dùng đã xác nhận, nội dung được chốt chính thức.

**Vị trí đặt:** Dòng đầu tiên của file, trước tiêu đề.

**Ví dụ:**
```text
Trang-thai: cho-duyet
```

**Quy tắc:**
- Khi tạo file mới hoặc hoàn thành nội dung → gán `Trang-thai: cho-duyet`.
- Khi người dùng xác nhận duyệt → cập nhật thành `Trang-thai: da-duyet`.
- Khi mở phiên chat mới, đọc trường `Trang-thai` để biết tiến độ hiện tại của từng file.

### Quy ước `Loai-noi-dung`

- `script-video-ngan`
- `script-video-dai`
- `post-social`
- `blog`
