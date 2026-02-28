Trang-thai: da-duyet

# Dàn Ý: Regex Cơ Bản Trong 1 Phút

**Tiêu đề:** Đây là đoạn code xấu nhất mà mình từng viết — 30 dòng if/else chỉ để kiểm tra mật khẩu

---

## 1) Vấn đề ngoại tại (Problem)

- **Hook (Câu mở đầu):** Đây là đoạn code xấu nhất mà mình từng viết. 30 dòng if/else lồng nhau, chỉ để kiểm tra mật khẩu có đủ mạnh hay không.
- **(Nhân) Vấn đề cụ thể:** Mỗi lần cần kiểm tra chuỗi ký tự (mật khẩu, số điện thoại, email...), bạn lại viết hàng chục dòng if/else lồng nhau: kiểm tra độ dài, kiểm tra có chữ hoa không, có số không, có ký tự đặc biệt không... Mỗi điều kiện một khối if riêng biệt. Mỗi điều kiện thêm một tầng phức tạp.
- **(Quả) Hậu quả bên ngoài hiện tại:** Code phình ra, rối rắm, khó đọc. Chỉ cần thay đổi một điều kiện nhỏ là phải sửa lại cả đống logic. Và khi có lỗi xảy ra, bạn phải ngồi dò từng dòng một để tìm xem sai ở chỗ nào. Tốn hàng giờ đồng hồ cho một việc lẽ ra chỉ mất vài giây.

## 2) Vấn đề nội tại (Agitate)

- **Cảm xúc chủ đạo:** Bạn nhìn thấy Regex trong code của người khác: một dòng ký hiệu ngắn gọn, giải quyết gọn ghẽ bài toán mà bạn phải viết 30 dòng. Bạn biết rõ mình đang lãng phí thời gian, nhưng nhìn vào những ký hiệu đó, bạn cảm thấy bất lực vì không hiểu chúng hoạt động như thế nào.
- **Niềm tin sai lệch:** "Regex quá phức tạp, chắc phải giỏi lắm mới dùng được" — trong khi thực tế, Regex chỉ là một bộ quy tắc đơn giản mà chưa có ai giải thích cho bạn bằng ngôn ngữ dễ hiểu.

## 3) Người dẫn đường (Guide)

- **Đồng cảm:** Mình hiểu cảm giác đó. Hồi mới học, mình cũng từng nhìn Regex rồi lập tức đóng tab lại vì sợ.
- **Giải oan:** Nhưng lỗi không phải do bạn không đủ khả năng. Lỗi là do bạn chưa được ai "dịch" Regex ra ngôn ngữ bình thường.

## 4) Giải pháp (The Solution)

### Kế hoạch — So sánh trực quan: 30 dòng if/else vs 1 dòng Regex

**Ví dụ: Kiểm tra mật khẩu mạnh** (ít nhất 8 ký tự, có chữ hoa, chữ thường, số, ký tự đặc biệt)

**BEFORE — 30 dòng if/else:**
```js
function validatePassword(password) {
  if (password.length < 8) return false;
  let hasUpper = false;
  let hasLower = false;
  let hasNumber = false;
  let hasSpecial = false;
  for (let i = 0; i < password.length; i++) {
    if (password[i] >= 'A' && password[i] <= 'Z') hasUpper = true;
    if (password[i] >= 'a' && password[i] <= 'z') hasLower = true;
    if (password[i] >= '0' && password[i] <= '9') hasNumber = true;
    if ('!@#$%^&*'.includes(password[i])) hasSpecial = true;
  }
  if (!hasUpper) return false;
  if (!hasLower) return false;
  if (!hasNumber) return false;
  if (!hasSpecial) return false;
  return true;
}
```

**AFTER — 1 dòng Regex:**
```js
/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[!@#$%^&*]).{8,}$/
```

**Giải mã từng phần (bóc tách chi tiết nhất):**

**Phần 1: `^` → "Bắt đầu từ đầu chuỗi"**
- Ký hiệu `^` có nghĩa là: bắt đầu kiểm tra từ ký tự đầu tiên của chuỗi. Không bỏ sót gì phía trước.

**Phần 2: `(?=.*[a-z])` → "Phải có ít nhất 1 chữ thường"**
- `?=` → Nghĩa là "hãy kiểm tra xem có tồn tại hay không", nhưng không tiêu thụ ký tự (chỉ nhìn trước, không dịch chuyển vị trí kiểm tra).
- `.*` → Dấu `.` đại diện cho một ký tự bất kỳ. Dấu `*` nghĩa là "lặp lại từ 0 đến vô hạn lần". Ghép lại: "bỏ qua bao nhiêu ký tự cũng được".
- `[a-z]` → Dấu ngoặc vuông `[]` nghĩa là "một trong các ký tự bên trong". `a-z` nghĩa là "từ a đến z". Ghép lại: "một chữ cái thường bất kỳ".
- Cả cụm: "Nhìn xuyên suốt chuỗi, kiểm tra xem có ít nhất 1 chữ thường hay không."

**Phần 3: `(?=.*[A-Z])` → "Phải có ít nhất 1 chữ hoa"**
- Tương tự phần 2, nhưng `[A-Z]` nghĩa là "từ A đến Z" → một chữ cái viết hoa bất kỳ.

**Phần 4: `(?=.*\d)` → "Phải có ít nhất 1 chữ số"**
- Tương tự phần 2, nhưng `\d` là viết tắt của "digit" → một chữ số bất kỳ (0-9).

**Phần 5: `(?=.*[!@#$%^&*])` → "Phải có ít nhất 1 ký tự đặc biệt"**
- Tương tự phần 2, nhưng `[!@#$%^&*]` liệt kê cụ thể các ký tự đặc biệt được chấp nhận.

**Phần 6: `.{8,}` → "Tổng cộng từ 8 ký tự trở lên"**
- `.` → Một ký tự bất kỳ.
- `{8,}` → Dấu ngoặc nhọn `{}` quy định số lần lặp. `8,` nghĩa là "ít nhất 8 lần, không giới hạn tối đa".
- Ghép lại: "chuỗi phải có từ 8 ký tự trở lên".

**Phần 7: `$` → "Kết thúc chuỗi"**
- Ký hiệu `$` có nghĩa là: kiểm tra đến ký tự cuối cùng. Không cho phép thừa gì phía sau.

**Thông điệp cốt lõi:** Regex không phải phép thuật. Mỗi ký hiệu đều có một ý nghĩa cụ thể. Khi bạn hiểu từng phần, cả dòng Regex trở nên dễ đọc như một câu tiếng Việt bình thường.

### CTA (Kêu gọi hành động)
- Muốn học Regex cùng lộ trình Full Stack bài bản? Xem chi tiết tại phần mô tả hoặc bình luận.

---

## Lưu ý khi viết script:
- Văn phong: Tự nhiên, gần gũi, giống đang trò chuyện. Không dùng từ lóng.
- Giữ đúng 1 ví dụ duy nhất (mật khẩu). Không lan man sang ví dụ khác.
- Hành trình cảm xúc: SỢ → HIỂU → TỰ TIN.
- Thời lượng mục tiêu: 1-3 phút.
