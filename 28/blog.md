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

### **Nguyên tắc 1: Tên phải thể hiện mục đích rõ ràng**

Đây là nguyên tắc quan trọng nhất. Khi nhìn vào tên biến, tên hàm, tên class,… nó phải cho chúng ta biết được ngay **mục đích dùng để làm gì?**

Bây giờ, mình sẽ áp dụng quy tắc này để sửa lại đoạn code sau.

Hiện tại, tên hàm `processData` có ý nghĩa quá chung chung. Nên mình sẽ đổi tên thành `calculateTotalRevenue`, tạm dịch là tính tổng doanh thu.

```jsx
// Before
function processData(arr) {
  // ...
}

// After
function calculateTotalRevenue(arr) {
  // ...
}
```

Để đổi tên một cách an toàn và đồng bộ, bạn nên dùng chức năng **Rename Symbol** của VS Code để toàn bộ nơi đang gọi hàm được cập nhật cùng lúc.

Như vậy, những nơi nào đang gọi hàm này trong dự án đều sẽ được tự động cập nhật theo. Mình sẽ không cần tốn nhiều thời gian để đi rà soát hay sửa thủ công từng chỗ.

Dù tên hàm hơi dài một chút, nhưng miễn sao nó thể hiện đúng mục đích là được

Bạn nên nhớ rằng: Nguyên tắc của Clean Code là ưu tiên sự rõ ràng hơn độ dài của tên.

Tiếp theo là tham số `arr`. Tại vì nó dùng để chứa danh sách các đơn hàng, nên mình sẽ đổi tên lại với mục đích rõ ràng hơn là `orders`.

Còn biến `temp` dùng để tính tổng giá trị của tất cả đơn hàng, nên mình sẽ đổi tên thành `totalRevenue`:

Biến `el` trong vòng lặp `forEach` tương ứng với mỗi đơn hàng trong mảng `orders`, nên mình sẽ đổi tên thành `order` dưới dạng số ít.

```jsx
// Trước
function processData(arr) {
  let temp = 0;
  arr.forEach(el => {
    // ...
  });
  return temp;
}

// Sau
function calculateTotalRevenue(orders) {
  let totalRevenue = 0;
  orders.forEach(order => {
    // ...
  });
  return totalRevenue;
}
```

Như vậy, sau khi áp dụng nguyên tắc thứ nhất, code của chúng ta đã trông rõ ràng hơn rất nhiều.

Mình có thể dễ dàng nắm bắt được logic tính tổng doanh thu như sau:

- Nếu đơn hàng nào thuộc loại **VIP** và có số lượng **trên 50**, thì tổng tiền của đơn hàng đó sẽ được **giảm 10%**.
- Ngược lại, nếu không thỏa điều kiện này thì giữ nguyên giá gốc.
Đến đây code đã khá ổn rồi. Tuy nhiên, nó vẫn còn một vấn đề nhỏ cần tối ưu. Đây là lúc mình cần sử dụng đến **nguyên tắc thứ 2: Loại bỏ Magic Number**.

## **Nguyên tắc thứ 2: Loại bỏ Magic Number**

Vậy Magic Number là gì?

Hiện tại trong mã nguồn có 2 con số `50` và `0.9`. Chúng chính là Magic Number.

Hiểu đơn giản, Magic Number là những con số được gán cứng trong mã nguồn mà không có tên gọi cụ thể.

Điều này khiến người đọc code nhìn vào sẽ không hiểu tại sao lại có con số đó và ý nghĩa của nó là gì. Để loại bỏ Magic number, mình sẽ đặt tên cho chúng.

Số `50` có ý nghĩa là số lượng mua tối thiểu để được giảm giá, nên mình sẽ khai báo một một hằng số có tên là `MIN_ORDER_FOR_DISCOUNT` để chứa giá trị `50`.

Tương tự, `0.9` là tỉ lệ giá sau khi đã giảm `10%` cho đơn hàng VIP, nên mình sẽ khai báo một hằng số có tên là `VIP_DISCOUNT_RATE` để chứa giá trị `0.9`.

```jsx
// Before
if (order.type === 'vip' && order.amount > 50) {
  totalRevenue += order.price * order.amount * 0.9;
}

// After
const MIN_ORDER_FOR_DISCOUNT = 50;
const VIP_DISCOUNT_RATE = 0.9;

if (order.type === 'vip' && order.amount > MIN_ORDER_FOR_DISCOUNT) {
  totalRevenue += order.price * order.amount * VIP_DISCOUNT_RATE;
}
```

Câu lệnh điều kiện bây giờ đã trở nên tường minh hơn rất nhiều.

Cách này không chỉ giúp code dễ đọc, mà còn **cực kỳ dễ bảo trì**. Sau này nếu cần thay đổi mức giảm giá hay số lượng, mình chỉ cần **sửa đúng một chỗ** tại vị trí khai báo biến, những nơi khác sử dụng các biến này cũng sẽ tự động được cập nhật theo.

### **Nguyên tắc số 3: Tên hàm phải là động từ**

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

Ở đây có một vấn đề rất rõ: logic kiểm tra user hợp lệ đang bị lặp ở cả `thanhToanDonHang` và `huyDonHang`.

Khi nghiệp vụ đổi, bạn sẽ phải sửa nhiều chỗ, rất dễ quên và gây lỗi.

### Phần code bị lặp

```jsx
// Bị lặp trong thanhToanDonHang
const user = users.find(u => u.id === userId);
if (!user) return "Lỗi: Không tìm thấy người dùng";
if (!user.isActive) return "Lỗi: Tài khoản bị khóa";

// Bị lặp trong huyDonHang
const user = users.find(u => u.id === userId);
if (!user) return "Lỗi: Không tìm thấy người dùng";
if (!user.isActive) return "Lỗi: Tài khoản bị khóa";
```

### Giải pháp: Tách logic dùng chung

```jsx
function layThongTinUserHopLe(userId) {
  const user = users.find(u => u.id === userId);

  if (!user) throw new Error("Không tìm thấy người dùng");
  if (!user.isActive) throw new Error("Tài khoản bị khóa");

  return user;
}
```

Hàm này chỉ làm đúng một việc:

- Nhận `userId`
- Kiểm tra điều kiện user hợp lệ
- Trả về `user` để các hàm khác dùng lại

### Áp dụng vào các nơi sử dụng

```jsx
function thanhToanDonHang(userId, items) {
  const user = layThongTinUserHopLe(userId);

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

function huyDonHang(userId, totalRefund) {
  const user = layThongTinUserHopLe(userId);

  user.balance += totalRefund;
  return "Hủy đơn thành công!";
}
```

### Khi có yêu cầu mới

Giả sử cần kiểm tra thêm email đã xác thực hay chưa, bạn chỉ cần sửa đúng một nơi:

```jsx
function layThongTinUserHopLe(userId) {
  const user = users.find(u => u.id === userId);

  if (!user) throw new Error("Không tìm thấy người dùng");
  if (!user.isActive) throw new Error("Tài khoản bị khóa");
  if (!user.isEmailVerified) throw new Error("Chưa xác thực email");

  return user;
}
```

Nhờ tách hàm, bạn sẽ có các lợi ích rất rõ:

- Chỉ sửa một chỗ khi nghiệp vụ thay đổi
- Giảm rủi ro sửa thiếu
- Code ngắn hơn, dễ đọc hơn
- Dễ viết test cho từng phần

Tóm lại, nếu trong mã nguồn có logic bị lặp ở nhiều nơi, hãy ưu tiên tách thành hàm riêng để tái sử dụng.

---

**Folder: Clip_04**

## 3. Thống nhất định dạng chung (Formatting)

10 giờ đêm, bạn đang chuẩn bị tắt máy thì bỗng nhiên nhận được cuộc gọi gấp từ Sếp:

“Chức năng giảm giá của hệ thống đang chạy sai cho hàng trăm đơn của khách hàng rồi. Em sửa gấp giúp anh trong hôm nay”.

Bạn vội vả mở file code, nhìn vào logic giảm giá mà mình vừa mới viết xong ngày hôm qua:

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

Mắt bạn dò từng dòng code. Bộ não bắt đầu làm việc quay cuồng chỉ để trả lời câu hỏi: Cái `else` này thuộc về `if` nào? Đơn hàng của khách hàng trên `1000` là giảm `20%` hay `10%`?

Bạn thật sự không ngờ rằng, mình lại đang khá vất vả để hiểu đoạn code vừa mới viết xong.

Vấn đề ở đây không phải bạn không hiểu rõ logic giảm giá như thế nào, mà do cấu trúc code khá lộn xộn, khiến bạn nhìn vào không phân biệt được đoạn code nào nằm bên trong đoạn code nào.

Mình biết rằng cảm giác lúc này của bạn cực kỳ khó chịu, khi mà mọi thứ đang trong tình trạng rất gấp.

Có thể trước đó bạn cho rằng code sao chạy được là được rồi, quan trọng gì định dạng xấu hay đẹp, khi nào rảnh thì chỉnh lại sau.

Nhưng khi dự án cần nâng cấp hoặc sửa lỗi, định dạng mã nguồn lộn xộn chính là nguyên nhân chính khiến bạn lãng phí rất phí rất nhiều thời gian và công sức.

Thay vì chỉ cần làm 10 phút là xong, giờ đây bạn lại tốn gần 1 tiếng, thậm chí cả một ngày làm việc. Tệ hơn là sửa một chỗ lại phát sinh lỗi ở hàng chục chỗ khác.

Vậy làm thế nào để định dạng code trở nên rõ ràng và dễ đọc hơn?

Dưới đây là 3 nguyên tắc CƠ BẢN NHẤT mà bạn có thể áp dụng ngay nếu muốn code của mình rõ ràng và dễ đọc:

**Nguyên tắc 1 - Nhất quán thụt lề**

Bạn hãy nhìn đoạn code sau:

```jsx
if (isValid) {
if (hasPermission) {
        processOrder();
}
}
```

Ở đây có hai câu lệnh `if` lồng nhau, nhưng do câu lệnh `if` bên trong không thụt lề vào nên cấu trúc rất khó nhìn.

Dẫn đến là bạn có thể sẽ không biết câu lệnh `if` bên trong là con của câu lệnh `if` bên ngoài, rồi hiểu sai logic.

Để cải thiện, mình chỉnh lại câu lệnh `if` bên trong thụt lề vào:

```jsx
if (isValid) {
  if (hasPermission) {
    processOrder();
  }
}
```

Lúc này, bạn nhìn vào là thấy ngay đoạn code nào là con và đoạn code nào là cha, và dễ dàng hiểu đúng logic hơn.

Nói chung các đoạn code con phải thụt lề vào để cấu trúc trở nên rõ ràng.

**Nguyên tắc 2 - Tách khối code theo ý nghĩa**

Hãy nhìn vào hàm `checkout` này:

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

Vấn đề ở đây là các câu lệnh đang dính liền một khối với nhau, bạn sẽ rất khó nhận biết nhanh logic tổng quan là gì.

Sau một tháng nhìn lại, bạn sẽ cảm thấy khá ngợp tại vì không biết đâu là phần kiểm tra ràng buộc? Đâu là phần tính tiền?

Cách đơn giản để cải thiện vấn đề này là mình sẽ tách các câu lệnh liên quan thành từng khối riêng biệt. Mỗi khối sẽ ngăn cách với nhau bằng một dấu khoảng cách.

Giả sử ở đây, mình có thể chia thành 3 khối.

Khối thứ nhất là các câu lệnh liên quan đến logic kiểm tra ràng buộc:

```jsx
function checkout(order) {
	if (!order || !order.items?.length) {
    throw new Error('Order is invalid');
  }
```

Khối thứ hai là các câu lệnh liên quan đến logic tính tiền:

```jsx
function checkout(order) {
	if (!order || !order.items?.length) {
    throw new Error('Order is invalid');
  }

	const subtotal = order.items.reduce((sum, item) => sum + item.price * item.qty, 0);
	const discount = order.isVip ? subtotal * 0.1 : 0;
	const finalTotal = subtotal - discount;
```

Và khối thứ ba là câu lệnh trả về kết quả cuối cùng:

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

Như bạn thấy, sau khi tách cách các câu lệnh liên quan thành từng khối riêng biệt, nội dung code đã trở nên tương minh hơn so với trước đó.

**Nguyên tắc 3 - Định dạng điều kiện phức tạp**

Hãy nhìn vào câu lệnh `if` này: Các điều kiện đang nằm cùng 1 dòng, trông rất rối mắt:

```jsx
if (order.isPaid && (order.type === 'vip' || order.total > 2000) && !order.isRefunded) {
  sendInvoice(order.id);
}
```

Bạn sẽ gặp khó khăn trong việc nhận biết có tổng cộng bao nhiêu điều kiện và thứ tự thực thi của chúng như thế nào.

Nếu cần chỉnh sửa hay bổ sung thêm điều kiện mới thì cũng rất dễ mắc sai sót.

Để giải quyết vấn đề này, rất đơn giản. Nếu có nhiều điều kiện, bạn chỉ cần định dạng lại cho mỗi điều kiện nằm trên một dòng riêng như sau:

```jsx
if (
  order.isPaid &&
  (order.type === 'vip' || order.total > 2000) &&
  !order.isRefunded
) {
  sendInvoice(order.id);
}
```

Lúc này, bạn sẽ dễ dàng nhận biết được có những điều kiện gì, và khi cần chỉnh sửa hoặc bổ sung thì mọi thứ cũng trở nên thuận tiện hơn.

Như vậy, bạn đã làm quen qua 3 nguyên tắc định dạng cơ bản nhất của Clean code.

Ngoài ra, còn rất nhiều nguyên tắc định dạng khác nữa. Ví dụ như: Giới hạn độ dài trên một dòng, xuống dòng khi gọi hàm có nhiều tham số, thứ tự các câu lệnh import,…

Nhưng tin vui là bạn không cần phải nhớ hết tất cả mọi thứ, chúng ta sẽ dùng công cụ để hỗ trợ một cách tự động. Nhờ vậy, mà cả nhóm sẽ thống nhất với nhau một định dạng chung khi làm việc.

**Công cụ thứ nhất mà mình muốn giới thiệu là ESLint.**

Chức năng của ESLint là thông báo lỗi nếu bạn hoặc ai đó vi phạm quy tắc chất lượng code đã được thống nhất từ trước. Ví dụ như đặt biến sai quy tắc, khai báo biến không dùng, sử dụng toán tử `==` thay vì `===`,…

**Công cụ thứ hai là Prettier:**

Đây là công cụ tự động điều chỉnh code theo đúng định dạng chuẩn.

Mỗi khi bạn viết code xong và lưu file, Prettier sẽ tự động định dạng lại thụt lề, xóa bỏ dòng trống dư thừa, sắp xếp lại vị trí đóng mở ngoặc cho phù hợp, thực hiện xuống dòng cho các điều kiện phức tạp… tất cả sẽ theo một chuẩn chung đã được cấu hình sẵn từ trước.

Khi dùng kết hợp ESLint và Prettier, bạn gần như tự động hoá 100% việc kiểm tra chất lượng code và thiết lập định dạng chung. Việc đọc code, sửa chữa và nâng cấp hệ thống sẽ trở nên thuận tiện và dễ dàng hơn rất nhiều.

Tuy nhiên, trong thực tế, có những đoạn code dù đã được định dạng rõ ràng nhưng vẫn khá khó hiểu. Bạn sẽ cần viết thêm ghi chú để sau này đọc lại và hiểu nhanh hơn.

Vậy viết ghi chú thế nào cho hiệu quả, đúng ý và không dư thừa? Chúng ta cùng tìm hiểu ở phần tiếp theo của video nhé.

---

**Folder: Clip_05**

## 4. Cách viết bình luận đúng cách trong mã nguồn (Comments)

Một ngày nọ, bạn nhận được một yêu cầu cập nhật lại logic tính phí vận chuyển. Mở code ra, bạn thấy hàm tính phí như sau:

```jsx
function calculateShippingFee(order) {
  const physicalItems = order.items.filter(item => item.type !== 'digital');

  if (physicalItems.length === 0) return 0;

  const totalWeight = physicalItems.reduce((sum, item) => sum + item.weight * item.qty, 0);
  const baseFee = totalWeight <= 3 ? 25000 : 25000 + Math.ceil((totalWeight - 3) / 0.5) * 3000;

  if (order.province === 'HCM' && order.shippingMethod === 'express') {
    return baseFee * 1.5;
  }

  return baseFee;
}
```

Nhìn vào đoạn code này, có thể bạn hiểu rõ logic tính toán, nhưng vẫn chưa rõ:

- Tại sao tổng cân nặng từ 3kg trở xuống thì phí giao hàng là 25.000đ, còn trên 3kg thì công thức tính lại khác?
- Hoặc tại sao giao hàng nhanh từ HCM lại nhân với 1.5?
Những con số này không phải ngẫu nhiên, chúng được lấy ra từ chính sách công ty mà bạn đang làm việc.

Nhưng ở đây không có bất kỳ ghi chú nào hết, bạn không biết chúng thật sự có ý nghĩa là gì. Chỉ cần vô tình sửa sai một chỗ, hệ thống của công ty sẽ tính sai hàng nghìn đơn hàng.

Để an toàn, bạn tiến hành thêm ghi chú chi tiết cho từng dòng code để sau này nhìn lại dễ hiểu hơn:

```jsx
// Tính phí vận chuyển
function calculateShippingFee(order) {
  // Lọc sản phẩm vật lý, bỏ qua sản phẩm số
  const physicalItems = order.items.filter(item => item.type !== 'digital');

  // Nếu không có sản phẩm vật lý thì phí là 0
  if (physicalItems.length === 0) return 0;

  // Tính tổng cân nặng của đơn hàng
  const totalWeight = physicalItems.reduce((sum, item) => sum + item.weight * item.qty, 0);
  // Tính phí vận chuyển dựa trên cân nặng
  const baseFee = totalWeight <= 3 ? 25000 : 25000 + Math.ceil((totalWeight - 3) / 0.5) * 3000;

  // Nếu là HCM và giao hàng nhanh thì nhân phí lên
  if (order.province === 'HCM' && order.shippingMethod === 'express') {
    return baseFee * 1.5;
  }

  // Trả về phí vận chuyển
  return baseFee;
}
```

Gần như mỗi dòng code đều có ghi chú. Nhưng việc ghi chú quá nhiều như thế này là không cần thiết, và lãng phí thời gian.

Tại vì phần lớn chúng chỉ đang lặp lại code một cách dư thừa. Do chỉ cần nhìn vào code là bạn có thể hiểu ngay logic mà không cần đọc ghi chú.

Thậm chí những câu hỏi quan trọng về nghiệp vụ trước đó vẫn còn bỏ ngỏ:

- Tại sao từ dưới 3kg lại tính phí ship khác so với trên 3kg.
- Tại sao ở HCM phí giao hàng nhanh lại nhân với 1.5?
Tồi tệ hơn, khi bạn thay đổi code mà quên cập nhật ghi chú, chúng sẽ phản tác dụng và khiến bạn hoặc đồng nghiệp hiểu sai hoàn toàn logic sau này.

Đây chính là vấn đề của việc ghi chú dư thừa.

Bạn bắt đầu bối rối. Không biết khi nào nên viết và không nên viết ghi chú…

Đừng lo lắng, ngay sau đây, mình sẽ hướng dẫn bạn viết ghi chú đúng cách.

Dưới đây là 3 nguyên tắc quan trọng mà bạn cần phải nắm.

**Nguyên tắc 1: Viết ghi chú để giải thích “TẠI SAO”, không phải là “CÁI GÌ”.**

Hãy nhìn vào đoạn code sau:

```jsx
// Tính phí vận chuyển
function calculateShippingFee(order) {
  // Lọc sản phẩm vật lý, bỏ qua sản phẩm số
  const physicalItems = order.items.filter(item => item.type !== 'digital');

  // Nếu không có sản phẩm vật lý thì phí là 0
  if (physicalItems.length === 0) return 0;

  // Tính tổng cân nặng của đơn hàng
  const totalWeight = physicalItems.reduce((sum, item) => sum + item.weight * item.qty, 0);
  // Tính phí vận chuyển dựa trên cân nặng
  const baseFee = totalWeight <= 3 ? 25000 : 25000 + Math.ceil((totalWeight - 3) / 0.5) * 3000;

  // Nếu là HCM và giao hàng nhanh thì nhân phí lên
  if (order.province === 'HCM' && order.shippingMethod === 'express') {
    return baseFee * 1.5;
  }

  // Trả về phí vận chuyển
  return baseFee;
}
```

Những ghi chú này không sai, nhưng chúng cũng hoàn toàn không cần thiết. Tại vì nhìn vào code, bạn có thể dễ dàng hiểu được ngay logic là gì.

Thay vào đó, bạn hãy viết ghi chú để trả lời câu hỏi “tại sao”, nghĩa là giải thích cho những logic nghiệp vụ đằng sau mà bản thân code không thể nào tự giải thích được.

Ví dụ như chỗ tính phí ship dựa trên tổng trọng lượng, mình sẽ thêm ghi chú nội dung nghiệp vụ như sau:

```jsx
function calculateShippingFee(order) {
  const physicalItems = order.items.filter(item => item.type !== 'digital');

  if (physicalItems.length === 0) return 0;

  const totalWeight = physicalItems.reduce((sum, item) => sum + item.weight * item.qty, 0);

  // Theo phụ lục hợp đồng GHN 2026-01:
  // - 25.000đ cho 3kg đầu
  // - Mỗi 0.5kg vượt thêm 3.000đ
  // Không tự ý đổi nếu chưa cập nhật bảng phí từ đối tác.
  const baseFee = totalWeight <= 3 ? 25000 : 25000 + Math.ceil((totalWeight - 3) / 0.5) * 3000;
```

Khi nhìn vào ghi chú này, bạn sẽ dễ dàng hiểu được tại sao phí ship lại được tính như vậy. Và bạn sẽ thận trọng hơn nếu muốn thay đổi công thức tính này.

Tương tự, mình sẽ thêm ghi chú nội dung nghiệp vụ giải thích lý do tại sao ở Hồ Chí Minh phải nhân với hệ số 1.5:

```jsx
  // Ngoại lệ tạm thời cho chiến dịch HCM Express (CRM-482), hiệu lực đến 2026-06-30.
  // Sau mốc này phải bỏ hệ số 1.5.
  if (order.province === 'HCM' && order.shippingMethod === 'express') {
    return baseFee * 1.5;
  }

  return baseFee;
}
```

Như vậy, mọi thứ đã rõ hơn. Các ghi chú đã giải thích nguồn gốc và bối cảnh của các con số. Đây là điều mà code không thể tự mình diễn đạt.

**Nguyên tắc 2 - Viết ghi chú để cảnh báo rủi ro**

Trong thực tế, có những đoạn code trông rất bình thường nhưng bạn không được phép thay đổi tùy tiện, nếu không hệ thống sẽ chạy sai ngay.

Để rõ hơn, bạn hãy nhìn vào ví dụ sau:

```jsx
const fields = ['id', 'createdAt', 'email', 'name'];
```

Giả sử mỗi phần tử trong mảng đang liên kết tương ứng với các cột trong file CSV của kế toán. Nếu mình hoặc ai đó không biết rồi vô tình thay đổi thứ tự thì dữ liệu của chương trình sẽ bị xáo trộn.

Để ngăn chặn vấn đề này, mình sẽ tiến hành viết ghi chú cảnh bảo rõ ràng như sau:

```jsx
// WARNING: Không đổi thứ giá trị, script import CSV của kế toán đang đọc theo đúng vị trí cột này. Đổi thứ tự sẽ gây nhập sai dữ liệu mà không có lỗi báo.
const fields = ['id', 'createdAt', 'email', 'name'];
```

Sau này mình hoặc đồng nghiệp nhìn vào là biết đây là đoạn code nhạy cảm và cần cẩn thận khi chỉnh sửa.

**Nguyên tắc 3 - Ưu tiên sửa tên biến hoặc tên hàm trước khi thêm ghi chú**

Bạn hãy nhìn đoạn code sau:

```jsx
// u là user
const u = userService.getById(id);
// x là điểm ưu tiên
const x = calc(u);
```

Nếu không có những dòng ghi chú, bạn sẽ không thể nào biết được biến `u` hay biến `x` có ý nghĩa là gì?

Nhưng việc viết ghi chú ở đây là hoàn toàn dư thừa.

Thay vào đó, mình sẽ xóa toàn bộ ghi chú và đổi lại tên biến cho rõ ràng hơn:

```jsx
const user = userService.getById(id);
const priorityScore = calculatePriorityScore(user);
```

Bây giờ, nhìn vào là hiểu ngay ý nghĩa của mỗi tên biến là gì.

Tóm lại, trước khi viết ghi chú, bạn hãy luôn đặt câu hỏi: Có thể đổi tên biến hoặc tên hàm trở nên rõ ràng hơn hay không?

Đến đây, bạn đã nắm được các kỹ thuật cơ bản nhất của Clean Code rồi đấy.

Nhưng sự thật là trong công việc hằng ngày, áp lực deadline thường khiến bạn sẽ khó lòng áp dụng Clean Code một cách hoàn hảo.

Vậy làm sao để cân bằng giữa Clean Code và deadline? Hãy cùng với mình tìm hiểu ở phần tiếp theo nhé.

---

**Folder: Clip_06**

## 6. Những lầm tưởng về Clean Code

Sau đây là những hiểu lầm tai hại về Clean Code mà chúng ta vẫn thường cho là đúng:

**Lầm tưởng 1 – Clean Code nghĩa là code phải hoàn hảo 100%**

Nếu bạn cho rằng khi làm dự án, mọi đoạn code phải luôn hoàn hảo 100%. Nhưng thực tế không phải như vậy.

Clean Code là sự cân bằng giữa dễ đọc, dễ bảo trì và đảm bảo dự án không bị chậm tiến độ.

Nếu bạn có một function đang chạy ổn định, không lỗi, và gần như rất ít khi chỉnh sửa.

Nhưng bạn vẫn dành hàng tiếng chỉ để đặt tên biến sao cho nghe có vẻ “hay hơn”. Đó không phải Clean Code, đó là sự lãng phí công sức, tiền bạc, và thời gian.

Clean Code không phải là code sao cho đẹp nhất, hoàn hảo nhất; mà là code vừa đủ rõ để bất kỳ ai cũng có thể dễ dàng đọc hiểu, và chỉnh sửa nó một cách nhanh chóng, và hiệu quả.

**Lầm tưởng 2 – Viết Clean Code luôn tốn thêm thời gian**

Nghe qua thì có vẻ hợp lý, vì bạn chắc chắn phải tốn thêm thời gian để làm rõ cách đặt tên và tối ưu lại cấu trúc code.

Và rồi, để làm cho nhanh hoặc áp lực deadline, bạn quyết định chọn cách viết đại sao cho code chạy được là xong.

Nhưng đó chính là cái bẫy của tư duy ngắn hạn: Bạn chỉ thấy mình tiết kiệm được chút thời gian bỏ ra hôm nay, mà quên đi cái giá rất đắt phải trả khi bảo trì dự án sau này.

Hãy nhìn đoạn code sau:

```jsx
function p(o, d) {
  const x = o.items.reduce((a, b) => a + b.p * b.q, 0);
  if (x > d) return null;
  return x;
}
```

Nếu ba tháng sau nhìn lại, bạn sẽ phải mất thời gian để hiểu: `p` là gì? `o` là gì? `x` là gì?

Nhưng nếu bạn đặt tên biến rõ ràng hơn:

```jsx
function calculateTotalPrice(order, maxBudget) {
  const totalPrice = order.items.reduce((sum, item) => sum + item.price * item.qty, 0);

  if (totalPrice > maxBudget) {
    return null;
  }

  return totalPrice;
}
```

Việc đặt tên biến rõ ràng hơn có thể chỉ tốn thêm 30 giây. Nhưng ba tháng sau, bạn có thể dễ dàng hiểu ngay thay vì phải tốn 10 đến 15 phút để giải mã lại đoạn code của chính mình.

**Lầm tưởng 3 – Clean Code chỉ cần thiết cho dự án lớn**

Một suy nghĩ rất phổ biến là: Dự án nhỏ thì không cần bận tâm đến Clean Code. Điều này có đúng không?

Có lẽ bạn đã từng viết vội một hàm dài hơn 200 dòng code chỉ với mục đích dùng tạm. Khi đó, bạn đặt tên biến khá sơ sài và không bận tâm nhiều đến việc sắp xếp cấu trúc code.

Ban đầu, mọi thứ hoạt động rất êm xuôi. Thế nhưng sáu tháng sau, khi dự án chỉ mới mở rộng thêm một chút và cần gắn thêm tính năng mới, không ai trong team dám đụng đến đoạn code đó nữa.

Lý do không phải vì logic bên trong quá cao siêu, mà đơn giản là vì... nhìn vào không ai hiểu gì cả!

Vì vậy, bạn không nên xem nhẹ những dự án nhỏ, vì chúng hoàn toàn có thể phát triển thành một hệ thống lớn sau này.

Việc giữ thói quen viết code rõ ràng ngay từ đầu chính là cách tốt nhất để bạn tiết kiệm được vô số thời gian và công sức bảo trì trong tương lai.

Để áp dụng Clean Code một cách hiệu quả trong dự án thực tế, đặc biệt là trong môi trường làm việc có deadline gấp, bạn chỉ cần áp dụng hai nguyên tắc sau.

**Nguyên tắc 1 – Áp dụng “Clean Code tối thiểu”**

Bạn hãy tập trung vào ba điều quan trọng nhất sau đây:

- Điều thứ nhất: Đặt tên rõ ràng.
- Điều thứ hai: Logic lặp lại ở nhiều nơi nên tách ra thành một hàm dùng chung.
- Cuối cùng là viết test cho những luồng logic quan trọng. Ví dụ như thanh toán, giỏ hàng, đăng ký, đăng nhập.
Như vậy là vừa đủ để code dễ đọc, dễ sửa mà không lo dự án bị chậm tiến độ.

**Nguyên tắc 2 – Luôn phải trả nợ kỹ thuật sớm nhất có thể.**

Trong thực tế, việc phải viết code 'chữa cháy' để kịp deadline là điều không thể tránh khỏi.

Tuy nhiên, bạn cần nhớ rằng: đã chấp nhận vay 'nợ kỹ thuật' thì phải có kế hoạch rõ ràng để trả nợ sớm nhất có thể.

Bạn không cần phải cố gắng trả hết nợ trong một lần, mà hãy chia nhỏ ra và cải thiện từng phần một, bắt đầu từ những khu vực bạn thường xuyên làm việc nhất.

Clean Code không phải là thứ bạn làm một lần cho xong. Nó là quá trình cải thiện liên tục.

Trong đó, mỗi thay đổi nhỏ sẽ dần tích lũy lại, tạo nên một nền tảng mã nguồn vững chắc lâu dài cho cả dự án.

---

**Folder: Clip_07**

## 7. Kết luận

Hy vọng qua video này, bạn đã nắm được những kiến thức nền tảng quan trọng nhất về Clean Code.

Khi áp dụng Clean Code mỗi ngày, bạn sẽ thấy code của mình đã trở nên dễ dàng kiểm soát và ít lỗi hơn so với trước đó.

Sếp và đồng nghiệp bắt đầu tin tưởng, và giao thêm cho bạn các dự án quan trọng hơn trong tương lai.

Tuy nhiên, nếu bạn cho rằng: Trong thời đại AI thì cần gì học Clean Code cho tốn thời gian, thì đó là một sai lầm.

AI chỉ giúp bạn viết code nhanh hơn. Nếu không có tư duy Clean Code, bạn sẽ rất khó kiểm soát và sửa lỗi trên một đống code khổng lồ do AI tạo ra.

Để thực sự làm chủ kỹ năng lập trình, và nhanh chóng xây dựng được một hệ thống hoàn chỉnh  từ con số 0; bạn có thể tham khảo các khóa học **1 kèm 1 của LetDiv** tại phần mô tả hoặc bình luận nhé.

