Trang-thai: cho-duyet

**Tiêu đề:** Đừng để Code Bẩn trở thành DẤU CHẤM HẾT cho sự nghiệp Dev của bạn!

---

**Folder: Clip_01**

Đừng để Code Bẩn trở thành DẤU CHẤM HẾT cho sự nghiệp lập trình của bạn!

Bạn đã từng bao giờ mất cả ngày trời để đọc lại đống code do chính mình viết cách đây 10 ngày, chỉ để sửa một lỗi nhỏ chưa?

Tệ hơn nữa, bạn sửa chỗ này lại phát sinh lỗi ở hàng loạt chỗ khác. Trang web ngày càng bất ổn, lỗi lặt vặt xuất hiện khắp nơi, deadline cận kề mà công việc vẫn dậm chân tại chỗ, còn sếp thì hối thúc tin nhắn liên tục.

Bạn bắt đầu cảm thấy căng thẳng, bất lực và bực bội. Tinh thần dần kiệt quệ, niềm đam mê với lập trình gần như đã biến mất. Công việc không còn mang lại niềm vui, mà giờ như là một cuộc chiến mỗi ngày.

Đây chính là hậu quả điển hình của Code Bẩn.

Mình hiểu cảm giác đó, vì mình cũng đã từng trải qua giống như bạn.

Vậy làm sao để code trở nên dễ đọc, dễ bảo trì, và mở rộng?

Sau hơn 10 năm làm việc và đọc qua nhiều cuốn sách về Clean Code, mình đã tổng hợp được những kỹ thuật thực chiến nhất mà bạn có thể áp dụng ngay vào dự án của mình sau khi xem xong video này.

Đặc biệt, mình còn sẽ hướng dẫn bạn cách tái cấu trúc mã an toàn cho những dự án cũ mà không cần phải đập đi xây lại từ đầu.

Okay, giờ thì chúng ta bắt đầu thôi.

---

**Folder: Clip_02**

## 1. Đặt tên (Naming)

Trước tiên, mình sẽ giới thiệu cho bạn kỹ thuật cơ bản nhất nhưng cũng là quan trọng nhất trong các kỹ thuật Clean Code đó là **Cách đặt tên**.

Khi mới học lập trình, hầu hết chúng ta đều có thói quen đặt tên biến rất tùy hứng. Thậm chí, ngay cả nhiều lập trình viên đã đi làm đôi khi vẫn mắc phải những lỗi này.

Nhìn vào đoạn code sau, bạn có hiểu nó đang thực hiện chức năng gì không?

```jsx
function processData(arr) {
  let temp = 0;
  arr.forEach(el => {
    if (el.type === 'vip' && el.amount > 50) {
      temp += el.price * el.amount * 0.9;
    } else {
      temp += el.price * el.amount;
    }
  });
  return temp;
}
```

Gần như rất khó để hình dung chức năng cụ thể của hàm này là gì nếu chỉ nhìn lướt qua.

Bạn phải đọc từng dòng lệnh, phân tích logic, và chạy chương trình nhiều lần mới lờ mờ đoán được là **“hình như nó đang tính tổng cái gì đó…”**.

Nếu mình không tiết lộ rằng hàm này dùng để **tính doanh thu dựa trên danh sách đơn hàng**, thì có lẽ bạn sẽ mất rất nhiều thời gian tìm hiểu.

Và tệ hơn, khi bạn cần sửa code, việc không hiểu rõ luồng logic cũ sẽ rất dễ dẫn đến việc tạo ra thêm nhiều lỗi khác.

Để giải quyết vấn đề này, chúng ta cần tuân thủ 3 nguyên tắc cốt lõi sau đây trong việc đặt tên.

**Nguyên tắc thứ nhất, tên phải thể hiện mục đích rõ ràng.**

Đây là nguyên tắc quan trọng nhất. Khi nhìn vào tên biến, tên hàm, tên class,… nó phải cho chúng ta biết được ngay **mục đích dùng để làm gì?**

Bây giờ, mình sẽ áp dụng quy tắc này để sửa lại đoạn code sau.

Hiện tại, tên hàm `processData` có ý nghĩa quá chung chung. Nên mình sẽ đổi tên thành `calculateTotalRevenue`, tạm dịch là tính tổng doanh thu.

Để đổi tên một cách an toàn và đồng bộ, mình đặt con trỏ chuột tại vị trí tên mà mình muốn đổi.

Sau đó bấm F2:

Lúc này, mình nhập tên mới:

Cuối cùng là bấm Enter:

Như vậy, những nơi nào đang gọi hàm này trong dự án đều sẽ được tự động cập nhật theo. Mình sẽ không cần tốn nhiều thời gian để đi rà soát hay sửa thủ công từng chỗ.

Dù tên hàm hơi dài một chút, nhưng miễn sao nó thể hiện đúng mục đích là được

Bạn nên nhớ rằng: Nguyên tắc của Clean Code là ưu tiên sự rõ ràng hơn độ dài của tên.

Tiếp theo là tham số `arr`. Tại vì nó dùng để chứa danh sách các đơn hàng, nên mình sẽ đổi tên lại với mục đích rõ ràng hơn là `orders`.

Còn biến `temp` dùng để tính tổng giá trị của tất cả đơn hàng, nên mình sẽ đổi tên thành `totalRevenue`:

Biến `el` trong vòng lặp `forEach` tương ứng với mỗi đơn hàng trong mảng `orders`, nên mình sẽ đổi tên thành `order` dưới dạng số ít.

Như vậy, sau khi áp dụng nguyên tắc thứ nhất, code của chúng ta đã trông rõ ràng hơn rất nhiều.

Mình có thể dễ dàng nắm bắt được logic tính tổng doanh thu như sau:

- Nếu đơn hàng nào thuộc loại **VIP** và có số lượng **trên 50**, thì tổng tiền của đơn hàng đó sẽ được **giảm 10%**.
- Ngược lại, nếu không thỏa điều kiện này thì giữ nguyên giá gốc.
Đến đây code đã khá ổn rồi. Tuy nhiên, nó vẫn còn một vấn đề nhỏ cần tối ưu. Đây là lúc mình cần sử dụng đến **nguyên tắc thứ 2: Loại bỏ Magic Number**.

Vậy Magic Number là gì?

Hiện tại trong mã nguồn có 2 con số **50** và **0.9**. Chúng chính là Magic Number.

Hiểu đơn giản, Magic Number là những con số được gán cứng trong mã nguồn mà không có tên gọi cụ thể.

Điều này khiến người đọc code nhìn vào sẽ không hiểu tại sao lại có con số đó và ý nghĩa của nó là gì. Để loại bỏ Magic number, mình sẽ đặt tên cho chúng.

Số **50** có ý nghĩa là số lượng mua tối thiểu để được giảm giá, nên mình sẽ khai báo một một hằng số có tên là **MIN_ORDER_FOR_DISCOUNT** để chứa giá trị **50**.

Tương tự, **0.9** là tỉ lệ giá sau khi đã giảm 10% cho đơn hàng VIP, nên mình sẽ khai báo một hằng số có tên là **VIP_DISCOUNT_RATE** để chứa giá trị **0.9**.

Câu lệnh điều kiện bây giờ đã trở nên tường minh hơn rất nhiều.

Cách này không chỉ giúp code dễ đọc, mà còn **cực kỳ dễ bảo trì**. Sau này nếu cần thay đổi mức giảm giá hay số lượng, mình chỉ cần **sửa đúng một chỗ** tại vị trí khai báo biến, những nơi khác sử dụng các biến này cũng sẽ tự động được cập nhật theo.

Cuối cùng là **nguyên tắc số 3: Tên hàm phải là động từ.**

Vì hàm đại diện cho một hành động cụ thể, nên tên của nó nhất định phải là động từ.

Ví dụ, hàm `calculateTotalRevenue` có tên là một động từ, và thể hiện đúng mục đích là dùng để tính tổng doanh thu.

Ngược lại, tên biến, tên class,… thì nên là danh từ.

Như vậy, chúng ta đã đi qua 3 nguyên tắc quan trọng nhất của kỹ thuật đặt tên biến. Chỉ cần nắm vững và thực hành thành thạo 3 nguyên tắc đặt tên này, code của bạn sẽ trở nên dễ đọc và chuyên nghiệp hơn 80% so với trước đây rồi đấy!

---

**Folder: Clip_03**

## 2. Tách hàm

"Sửa gấp giúp anh hiển thị ngày tháng trong hệ thống để phù hợp với định dạng bên Nhật nhé, 1 tiếng sau anh phải họp với đối tác rồi!" - Sếp vội vã chỉ tay vào màn hình và nói.

"Okay, 30 phút sau có ngay cho anh ạ!" - Bạn trả lời một cách đầy tự tin. Sau đó mở ứng dụng VS Code lên, rồi nhanh chóng bắt tay vào công việc.

Bỗng nhiên bạn khựng lại, 2 tay ôm lấy đầu, miệng há hốc vì biết mình đang gặp một vấn đề nghiêm trọng:

"Chết rồi! Nếu muốn sửa định dạng ngày tháng, mình phải sửa lại code của màn hình danh sách sản phẩm, chi tiết sản phẩm, giỏ hàng,… và rất nhiều màn hình khác nữa…"

Với một hệ thống có hơn hàng trăm màn hình, bạn ước lượng làm một ngày chưa chắc đã xong, 1 tiếng sao mà kịp… Tệ hơn, bạn có thể sửa thiếu hoặc vô tình sửa nhầm logic của chức năng khác.

Bạn nhận ra hệ thống đang vi phạm nguyên tắc code bị trùng lặp ở nhiều nơi. Mỗi lần cần chỉnh sửa đơn giản đều biến thành một nhiệm vụ tốn thời gian, và tiềm ẩn đầy rủi ro.

Giải pháp ở đây, bạn chỉ cần tách các đoạn code trùng lặp ra thành một hàm tiện ích dùng chung. Những nơi nào cần sử dụng thì chỉ cần gọi hàm tiện ích này ra.

Sau này cần chỉnh sửa, bạn chỉ cần chỉnh sửa bên trong hàm tiện ích này, các nơi khác sẽ tự động được cập nhật theo.

Để giúp bạn dễ hình dung, mình có một ví dụ đơn giản như sau:

```jsx
// Giả lập cơ sở dữ liệu
const users = [{ id: 1, name: "An", balance: 500, isActive: true }];
const products = [{ id: 101, name: "Laptop", price: 200, stock: 5 }];

// 1. Chức năng thanh toán
function thanhToanDonHang(userId, items) {
    const user = users.find(u => u.id === userId);
    if (!user) return "Lỗi: Không tìm thấy người dùng";
    if (!user.isActive) return "Lỗi: Tài khoản bị khóa";

    let tongTien = 0;
    for (let i = 0; i < items.length; i++) {
        const product = products.find(p => p.id === items[i].id);
        if (!product || product.stock < items[i].quantity) {
            return "Lỗi: Sản phẩm " + items[i].id + " không đủ hàng";
        }
        tongTien += product.price * items[i].quantity;
    }

    if (user.balance < tongTien) return "Lỗi: Không đủ tiền";
    user.balance -= tongTien;
    return "Thanh toán thành công!";
}

// 2. Chức năng hủy đơn (Để hoàn tiền)
function huyDonHang(userId, totalRefund) {
    const user = users.find(u => u.id === userId);
    if (!user) return "Lỗi: Không tìm thấy người dùng";
    if (!user.isActive) return "Lỗi: Tài khoản bị khóa";

    user.balance += totalRefund;
    return "Hủy đơn thành công!";
}
```

Ở đây, mình có mảng chứa thông tin danh sách người dùng và mảng chứa thông tin danh sách sản phẩm.

Tiếp theo, mình có hàm thanh toán đơn hàng và hàm hủy đơn hàng.

Bên trong hàm hủy đơn hàng, mình có logic lấy thông tin người dùng dựa trên userId và kiểm tra xem người có hợp lệ hay không.

Và bên trong hàm thanh toán đơn hàng cũng có logic bị lặp lại tương tự như vậy.

Nếu sau này, sếp hoặc khách hàng yêu cầu bổ sung thêm logic kiểm tra xem người dùng đã xác thực email hay chưa, **thì mình **cần phải sửa **ít nhất hai nơi**.

Thứ nhất là bên trong hàm thanh toán đơn hàng và thứ hai là bên trong hàm hủy đơn hàng.

Quên một chỗ là chương trình chạy sai ngay.

Để giải quyết vấn đề này, mình sẽ tiến hành gom logic trùng lặp vào một hàm dùng chung.

Đầu tiên, mình tạo một hàm mới có tên là `layThongTinUserHopLe`:

```jsx
function layThongTinUserHopLe(userId) {
	
}
```

Sau đó, mình sẽ chuyển logic trùng lặp vào bên trong hàm này:

```diff
function layThongTinUserHopLe(userId) {
+	const user = users.find(u => u.id === userId);
+	if (!user) throw new Error("Không tìm thấy người dùng");
+ if (!user.isActive) throw new Error("Tài khoản bị khóa");

+	return user;	
}
```

Hàm này chỉ làm đúng một việc: Nhận `userId`, kiểm tra các điều kiện cần thiết, và cuối cùng là trả về thông tin người dùng ****hợp lệ.

Tiếp theo, mình sẽ gọi hàm lấy thông tin user hợp lệ tại những nơi cần sử dụng.

Đầu tiên, là gọi bên trong hàm thanh toán đơn hàng:

```diff
function thanhToanDonHang(userId, items) {
-	const user = users.find(u => u.id === userId);
-	if (!user) return"Lỗi: Không tìm thấy người dùng";
-	if (!user.isActive) return"Lỗi: Tài khoản bị khóa";
+	const user = layThongTinUserHopLe(userId);

  let tongTien = 0;
```

Thứ hai, là gọi bên trong hàm hủy đơn hàng:

```diff
function huyDonHang(userId, totalRefund) {
-	const user = users.find(u => u.id === userId);
-	if (!user)return"Lỗi: Không tìm thấy người dùng";
-	if (!user.isActive)return"Lỗi: Tài khoản bị khóa";
+	const user = layThongTinUserHopLe(userId);
	
	 user.balance += totalRefund;
	 return "Hủy đơn thành công!";
}
```

Giả sử, sau này có tình huống bổ sung thêm logic kiểm tra người dùng đã xác thực email hay chưa, mình chỉ cần thêm code vào hàm lấy thông tin user hợp lệ là xong:

```diff
function layThongTinUserHopLe(userId) {
	const user = users.find(u => u.id === userId);
	
	if (!user) throw new Error("Không tìm thấy người dùng");
	if (!user.isActive) throw new Error("Tài khoản bị khóa");
+ if (!user.isEmailVerified) throw new Error("Chưa xác thực email");
	
	return user;
}
```

Nhờ vào việc tách các logic trùng lặp ra một hàm riêng, mỗi lần có chỉnh sửa, mình chỉ cần chỉnh sửa một nơi, những nơi khác sẽ tự động cập nhật theo mà không cần lo lắng có sửa thiếu hay không.

Tóm lại, khi bên trong mã nguồn của bạn có nhiều logic trùng lặp, bạn hãy cân nhắc tách thành hàm riêng để tái sử dụng, việc này sẽ giúp hệ thống dễ bảo trì hơn.

---

**Folder: Clip_04**

## 3. Thống nhất định dạng chung (Formatting)