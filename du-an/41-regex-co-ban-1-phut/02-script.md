Trang-thai: cho-duyet

# Script

**Tiêu đề:** Đây là đoạn code xấu nhất mình từng viết — 30 dòng if/else

---

Đây là đoạn code xấu nhất mà mình từng viết.

30 dòng if/else lồng nhau, chỉ để kiểm tra một thứ đơn giản: mật khẩu của người dùng có đủ mạnh hay không.

Kiểm tra độ dài, kiểm tra có chữ hoa không, có chữ thường không, có số không, có ký tự đặc biệt không... Mỗi điều kiện một khối if riêng biệt. Mỗi điều kiện thêm một tầng phức tạp.

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

Code phình ra, rối rắm, khó đọc. Chỉ cần thay đổi một điều kiện nhỏ là phải sửa lại cả đống logic. Và khi có lỗi xảy ra, bạn phải ngồi dò từng dòng một để tìm xem sai ở chỗ nào.

Tốn hàng giờ đồng hồ cho một việc lẽ ra chỉ mất vài giây.

Bạn biết rõ mình đang lãng phí thời gian. Bạn cũng từng nhìn thấy Regex trong code của người khác: một dòng ký hiệu ngắn gọn, giải quyết trọn vẹn bài toán mà bạn phải viết 30 dòng.

Nhưng nhìn vào những ký hiệu đó, bạn cảm thấy bất lực vì không hiểu chúng hoạt động như thế nào.

Mình hiểu cảm giác đó. Hồi mới học, mình cũng từng nhìn Regex rồi lập tức đóng tab lại vì sợ.

Nhưng lỗi không phải do bạn không đủ khả năng. Lỗi là do chưa có ai dịch Regex ra ngôn ngữ bình thường cho bạn.

Bây giờ mình sẽ làm điều đó.

Toàn bộ 30 dòng if/else phía trên, chỉ cần đúng 1 dòng Regex duy nhất là thay thế được toàn bộ:

```js
/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[!@#$%^&*]).{8,}$/
```

Nhìn vào đây, bạn có thể nghĩ rằng đây là một mớ ký hiệu vô nghĩa. Nhưng thực tế, mỗi ký hiệu đều có một ý nghĩa rất cụ thể. Mình sẽ bóc tách từng phần một cho bạn xem.

Đầu tiên, ký hiệu `^` ở đầu, có nghĩa là: bắt đầu kiểm tra từ ký tự đầu tiên của chuỗi.

Tiếp theo, cụm `(?=.*[a-z])`. Hãy bóc tách từng thành phần từ từ:

Thứ nhất, `[a-z]` đơn giản nhất: "một chữ cái thường bất kỳ, từ a đến z". Ví dụ `[a-z]` sẽ khớp với `b`, `c`, `x`… nhưng không khớp với `A`, `3` hay `!`.

Thứ hai, `.*` nghĩa là "bỏ qua bao nhiêu ký tự cũng được". Dấu `.` là "một ký tự bất kỳ", dấu `*` là "bao nhiêu lần cũng được". Ví dụ chuỗi `Abc123!@` có 8 ký tự, dấu `.*` cho phép bạn lướt qua tất cả chúng để tìm thứ bạn cần.

Thứ ba, `?=` đơn giản là kiểm tra xem có hay không, mà không "tiêu thụ" ký tự nào. Chuỗi `a1`, khi kiểm tra `(?=.*[a-z])`, nó lướt qua (`.*`) tìm chữ thường (`[a-z]`) → tìm thấy `a` → "có, đạt". Nhưng kế tiếp, khi kiểm tra `(?=.*[A-Z])` (tìm chữ hoa), nó vẫn bắt đầu từ đầu chuỗi `a1` để tìm, chứ không bắt đầu từ vị trí trước đó.

Ghép cả cụm lại: `(?=.*[a-z])` = "Tìm xuyên suốt chuỗi xem có chữ thường hay không, nhưng không tiêu mất ký tự nào."

Tương tự, `(?=.*[A-Z])` kiểm tra có ít nhất 1 chữ hoa.

`(?=.*\d)` kiểm tra có ít nhất 1 chữ số. Ở đây `\d` là viết tắt của "digit", tức là chữ số từ 0 đến 9.

`(?=.*[!@#$%^&*])` kiểm tra có ít nhất 1 ký tự đặc biệt trong danh sách được liệt kê.

Tiếp theo, `.{8,}` nghĩa là chuỗi phải có từ 8 ký tự trở lên. Dấu ngoặc nhọn `{}` quy định số lần lặp, `8,` nghĩa là ít nhất 8 lần, không giới hạn tối đa.

Cuối cùng, ký hiệu `$` có nghĩa là kiểm tra đến ký tự cuối cùng của chuỗi.

Bạn thấy không? Regex không phải phép thuật. Mỗi ký hiệu đều có một ý nghĩa cụ thể. Khi bạn hiểu từng phần, cả dòng Regex trở nên dễ đọc như một câu bình thường.

Muốn học Regex cùng lộ trình Full Stack bài bản? Xem chi tiết tại phần mô tả hoặc bình luận.
