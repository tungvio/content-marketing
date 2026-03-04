**Folder: Clip_04**

## 4. Thống nhất định dạng chung (Formatting)

Tối thứ 6, khoảng hơn 10 giờ đêm, bạn đang chuẩn bị tắt máy thì thông báo nhảy liên tục. Production báo lỗi tính tiền sai, khách VIP vẫn bị tính full giá. Sếp nhắn tin rất nhanh cho bạn: “Em hotfix gấp giúp anh trong 30 phút nhé.” Bạn gật đầu và bắt đầu mở file `applyDiscount.js` và thật bất ngờ.

Trên màn hình là một đoạn code trông như thế này:

```jsx
function applyDiscount(order){
if(order.isVip)
{if(order.total>1000)
return order.total*0.8
else
return order.total*0.9}
else{return order.total}
}
```

Bạn đứng hình vài giây. Bộ não bắt đầu làm việc quay cuồng chỉ để trả lời cho câu hỏi: Cái `else` này thuộc về `if` nào? Nhánh VIP trên 1000 là giảm 20% hay 10%? Có thiếu ngoặc không?. Thời gian thì vẫn cứ chạy. Bạn thì đọc nhanh qua, hiểu theo cách bạn cho là hợp lý nhất, sửa lại điều kiện và triển khai.

Năm phút sau, thông báo lại hiện lên: “Khách thường lại bị giảm giá.” Thế nguyên đoạn code bị rollback. Cả team phải tăng ca chỉ để đọc lại logic, dò lại từng nhánh điều kiện xem thực sự chuyện gì đang xảy ra.

Vấn đề ở đây không phải bạn không biết nghiệp vụ. Bạn hiểu rất rõ giảm giá cho VIP là như thế nào. Nhưng bạn không biết mình có đang hiểu đúng cấu trúc code hay không. Bạn không sai vì thiếu kiến thức, bạn sai vì… đọc nhầm. Và cảm giác đó cực kỳ khó chịu, khi mà mọi thứ đang rất gấp.

Rất nhiều người khi mới học nghĩ rằng formatting chỉ là vấn đề thẩm mỹ, họ chỉ cần code chạy là được, khi rảnh thì chỉnh lại sau. Nhưng họ đâu biết khi một dự án “cháy” vào lúc 10 giờ đêm, định dạng sẽ là thứ giúp bạn nhìn vào và hiểu vấn đề ngay lập tức.

Dưới đây là 3 nguyên tắc định dạng CƠ BẢN NHẤT mà bạn nên nhớ và áp dụng nếu muốn code của mình rõ ràng, dễ đọc và ít gây hiểu nhầm trong những tình huống quan trọng:

- **Nguyên tắc 1 - Nhất quán thụt lề**

- **Cái gì?** Một cấp logic = một cấp thụt lề, không trộn tab và space.
- **Tại sao?** Thụt lề chính là bản đồ cấu trúc code; nhìn vào là biết scope đang nằm ở đâu, `else` thuộc `if` nào.
- **Làm thế nào?** Chọn một chuẩn indent duy nhất cho toàn repo và giữ nhất quán trong mọi file.

Ví dụ trước khi chỉnh sửa, đoạn code có thể trông như thế này:

```jsx
if (isValid) {
if (hasPermission) {
	processOrder();
}
  }
```

Về mặt logic, thì đoạn code trên nó không sai. Nhưng về mặt đọc hiểu, nó bắt đầu có vấn đề.  Bạn nhìn vào hai cái  `if` và dấu  `{}`  các câu hỏi thay nhau hiện lên: `processOrder()` thuộc về `if` nào? Có bao nhiêu block đang mở?Liệu có đang thiếu một dấu đóng ngoặc ở đâu không?. Code thì vẫn chạy nhưng việc bạn xác định cấu trúc trở nên khó khăn.

Nhưng chỉ cần chỉnh lại thụt lề cho nhất quán:

```jsx
if (isValid) {
	if (hasPermission) {
		processOrder();
  }
}
```

Nhìn vào là hiểu ngay cấu trúc lồng nhau, không cần suy đoán.

- **Nguyên tắc 2 - Tách block theo ý nghĩa**

- **Cái gì?** Dùng dòng trống để tách các cụm: validation, business logic, return.
- **Tại sao?** Não đọc theo “cụm ý”, không đọc từng dòng rời rạc.
- **Làm thế nào?** Mỗi đoạn chỉ làm một nhiệm vụ và đứng thành block riêng.

Đừng để các block dính liền vào nhau như một khối đặc. Não chúng ta không đọc từng dòng rời rạc, mà đọc theo “cụm ý”. Nếu bạn không tách các cụm đó ra bằng dòng trống hoặc comment ngắn gọn, khi đọc bạn sẽ phải tự phân tách chúng trong đầu và điều đó tốn năng lượng không cần thiết.

Một hàm `checkout` rất đơn giản có thể được viết liền mạch như thế này:

```jsx
function checkout(order) {
	if (!order || !order.items?.length) {
		throw new Error('Order is invalid');
  }
	const subtotal = order.items.reduce((sum, item) => sum + item.price * item.qty, 0);
	const discount = order.isVip ? subtotal * 0.1 : 0;
	const finalTotal = subtotal - discount;
	return finalTotal;
}
```

Nó vẫn chạy đúng, không lỗi, không cảnh báo. Nhưng khi bạn mở lại sau vài tháng, cảm giác đầu tiên không phải “gọn gàng” mà  nó khá “ngợp” khi bạn phải tự chia đoạn trong đầu: Đâu là validation? Đâu là phần tính tiền? Đâu là kết quả cuối cùng?. 

Nếu ban đầu bạn tách thành các block rõ ràng:

```jsx
function checkout(order) {
	// Validation
	if (!order || !order.items?.length) {
		throw new Error('Order is invalid');
  }

	// Business logic
	const subtotal = order.items.reduce((sum, item) => sum + item.price * item.qty, 0);
	const discount = order.isVip ? subtotal * 0.1 : 0;
	const finalTotal = subtotal - discount;

	// Return
	return finalTotal;
}
```

Lần này khi bạn đọc lại, mắt của bạn sẽ di chuyển theo từng khối được tách sẵn. Luồng suy nghĩ lập tức rõ ràng: đầu tiên là kiểm tra sau đó đến tính toán và cuối cùng sẽ là trả kết quả.

- **Nguyên tắc 3 - Định dạng điều kiện phức tạp có chủ đích:**

- **Cái gì?** Với `if` nhiều điều kiện, xuống dòng và canh lề rõ ràng.
- **Tại sao?** Tránh đọc nhầm `&&`/`||` và thứ tự ưu tiên.
- **Làm thế nào?** Mỗi cụm điều kiện dài đặt trên một dòng để dễ rà soát.

Có những lúc bạn viết một câu `if` và nghĩ: “Chỉ thêm một điều kiện nữa thôi, không vấn đề gì đâu”. Rồi thêm một cái `&&` ,thêm một cặp ngoặc, thêm một điều kiện ngoại lệ. Và cuối cùng nó trông như thế này:

```jsx
if (order.isPaid && (order.type === 'vip' || order.total > 2000) && !order.isRefunded) {
  sendInvoice(order.id);
}
```

Theo logic thì không sai nhưng khi đồng nghiệp bạn nhìn vào và sẽ hỏi:  Điều kiện nào đi với điều kiện nào? Dấu `!` này đang phủ định cái gì? Cặp ngoặc này đóng ở đâu?. Bạn bắt đầu đọc lại, và không chắc bạn đang hiểu đúng hay không.

Khi bạn xuống dòng  chủ đích:

```jsx
if (
  order.isPaid &&
  (order.type === 'vip' || order.total > 2000) &&
  !order.isRefunded
) {
  sendInvoice(order.id);
}
```

Mỗi điều kiện lúc này giống như một mục trong danh sách. Bạn có thể rà soát từng dòng một cách bình tĩnh, thay vì cố gắng giải mã một chuỗi dài trên cùng một hàng.

Thực tế còn rất nhiều quy tắc định dạng khác như: giới hạn độ dài dòng, cách xuống dòng khi gọi hàm nhiều tham số, khoảng cách giữa các function hay thứ tự import. 

Nhưng tin vui là: bạn không cần phải nhớ hết tất cả những thứ đó, hãy để tool làm việc đó cho bạn. Kết quả là cả team không cần tốn thời gian tranh luận xem nên định dạng thế nào, mà có thể tập trung 100% vào logic và giải quyết bài toán thực sự.

- **ESLint - Cảnh báo lỗi code và formatting issues**

ESLint không chỉ là kiểm tra định dạng, mà còn phát hiện những lỗi tiềm ẩn trong code như khai báo biến nhưng không dùng, thiếu return trong một nhánh điều kiện, hay sử dụng `==` thay vì `===`. Nó giống như một lớp kiểm tra tự động, giúp bạn bắt bug sớm và đảm bảo mọi người trong team tuân theo cùng một bộ quy tắc.

- **Prettier - Auto-format code theo chuẩn:**

Nếu ESLint giống như người nhắc nhở quy tắc, thì Prettier giống như người tự động chỉnh sửa lại mọi thứ cho đúng chuẩn. Bạn có thể viết code theo thói quen của mình, nhưng mỗi lần save file, Prettier sẽ tự format lại: thụt lề, dòng trống, vị trí ngoặc, xuống dòng… tất cả theo một chuẩn chung đã được cấu hình sẵn.

Khi bạn dùng kết hợp ESLint và Prettier, bạn gần như tự động hoá 100% phần định dạng. Team không còn phải tranh luận chuyện “đặt ngoặc ở đâu”, “indent mấy space”, mà có thể dành toàn bộ năng lượng cho logic và kiến trúc hệ thống.

Định dạng không chỉ để code trông đẹp hơn. Nó giúp bạn tránh đọc sai, hiểu sai và sửa sai. Khi sự cố gấp xảy ra, team nhìn code là hiểu luồng ngay, fix đúng ngay lần đầu thay vì phải rollback nhiều lần.

Khi định dạng đã rõ ràng và nhất quán, bước tiếp theo không còn là “code trông thế nào”, mà là “người khác hiểu nó ra sao”. Đó là lúc chúng ta cần biết viết comment như thế nào cho đúng, để giúp code rõ ràng hơn.