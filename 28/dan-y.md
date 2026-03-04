**Folder: Clip_04**

## 4. Thống nhất định dạng chung (Formatting)

### Vấn đề ngoại tại (Tình huống)

Tối thứ 6, ngay trước giờ release, production báo lỗi tính tiền sai. Bạn được giao hotfix trong 30 phút.

Bạn mở đúng file cần sửa, nhưng đoạn `if/else` bị format lộn xộn: thụt lề không nhất quán, xuống dòng rối, block nhìn không rõ scope.

**Ví dụ JS (trước/sau):**

```jsx
// Trước: format rối, dễ đọc nhầm luồng
function applyDiscount(order){
if(order.isVip)
{if(order.total>1000)
return order.total*0.8
else
return order.total*0.9}
else{return order.total}
}

// Sau: format rõ ràng, nhìn là hiểu nhánh xử lý
function applyDiscount(order) {
  if (order.isVip) {
    if (order.total > 1000) {
      return order.total * 0.8;
    }

    return order.total * 0.9;
  }

  return order.total;
}
```

Bạn đọc nhầm luồng xử lý, sửa sai nhánh điều kiện. Hotfix deploy xong thì lỗi không hết, còn làm phát sinh lỗi mới.

Từ một bug nhỏ, team mất thêm vài giờ chỉ để rollback và truy lại logic thực tế.

### Vấn đề nội tại (Cảm xúc)

**Cảm giác thường gặp:**

- Căng thẳng vì deadline sát nút nhưng code nhìn vào không chắc mình đang hiểu đúng.
- Mất tự tin khi nhận ra lỗi đến từ việc đọc nhầm cấu trúc code chứ không phải thiếu kiến thức nghiệp vụ.

**Niềm tin sai lệch:**

- “Formatting chỉ là chuyện thẩm mỹ.”
- “Miễn code chạy thì format thế nào cũng được.”

### Giải pháp (Solution)

**Dưới đây là 3 nguyên tắc định dạng CƠ BẢN NHẤT** mà bạn nên nhớ và áp dụng ngay:

- **Nguyên tắc 1 - Nhất quán thụt lề (Indentation Consistency):**
    - **Cái gì?** Một cấp logic = một cấp thụt lề, không trộn tab/space.
    - **Tại sao?** Giúp nhìn vào là biết scope đang nằm ở đâu.
    - **Làm thế nào?** Chọn một chuẩn indent duy nhất cho toàn repo.
    - **Ví dụ JS (trước/sau):**
        
        ```jsx
        // Trước: khó nhìn scope (indent lộn xộn)
        if (isValid) {
        if (hasPermission) {
                processOrder();
        }
          }
        
        // Sau: scope rõ ràng
        if (isValid) {
          if (hasPermission) {
            processOrder();
          }
        }
        ```
        
- **Nguyên tắc 2 - Tách block theo ý nghĩa (Visual Grouping):**
    - **Cái gì?** Dùng dòng trống để tách validation, business logic, return.
    - **Tại sao?** Não đọc theo “cụm ý”, không đọc từng dòng rời rạc.
    - **Làm thế nào?** Mỗi đoạn làm một nhiệm vụ thì gom thành một block riêng.
    - **Ví dụ JS (trước/sau):**
        
        ```jsx
        // Trước: không có dòng trống, khó phân biệt validation/logic/return
        function checkout(order) {
          if (!order || !order.items?.length) {
            throw new Error('Order is invalid');
          }
          const subtotal = order.items.reduce((sum, item) => sum + item.price * item.qty, 0);
          const discount = order.isVip ? subtotal * 0.1 : 0;
          const finalTotal = subtotal - discount;
          return finalTotal;
        }
        
        // Sau: tách block rõ ràng theo ý nghĩa
        function checkout(order) {
          // Block 1: Validation - kiểm tra đầu vào
          if (!order || !order.items?.length) {
            throw new Error('Order is invalid');
          }
        
          // Block 2: Business logic - tính toán giá
          const subtotal = order.items.reduce((sum, item) => sum + item.price * item.qty, 0);
          const discount = order.isVip ? subtotal * 0.1 : 0;
          const finalTotal = subtotal - discount;
        
          // Block 3: Return kết quả
          return finalTotal;
        }
        ```
        
- **Nguyên tắc 3 - Định dạng điều kiện phức tạp có chủ đích:**
    - **Cái gì?** Xuống dòng, canh lề, đặt ngoặc rõ khi `if` nhiều điều kiện.
    - **Tại sao?** Tránh đọc nhầm `&&`/`||` và thứ tự ưu tiên.
    - **Làm thế nào?** Mỗi nhánh điều kiện dài nên tách thành một dòng dễ kiểm tra.
    - **Ví dụ JS (trước/sau):**
        
        ```jsx
        // Trước: điều kiện phức tạp nằm trên một dòng
        if (order.isPaid && (order.type === 'vip' || order.total > 2000) && !order.isRefunded) {
          sendInvoice(order.id);
        }
        
        // Sau: điều kiện phức tạp được xuống dòng có chủ đích
        if (
          order.isPaid &&
          (order.type === 'vip' || order.total > 2000) &&
          !order.isRefunded
        ) {
          sendInvoice(order.id);
        }
        ```
        
- **Còn nguyên tắc nào khác không?**
    
    Thực tế còn rất nhiều nguyên tắc formatting khác như:
    
    - Giới hạn độ dài dòng (line width)
    - Cách xuống dòng khi gọi hàm nhiều tham số
    - Khoảng cách giữa các function
    - Thứ tự sắp xếp import statements
    - ...và hàng chục quy tắc nhỏ khác
    
    **Nhưng bạn KHÔNG CẦN nhớ hết!** Vì có công cụ giúp tự động hoá toàn bộ phần này.
    
- **Hai công cụ giúp tự động hoá formatting:**
    - **Lợi ích:** Không cần nhớ qua nhiều nguyên tắc → để tool lo.
    - **Kết quả:** Team không tốn thời gian để suy nghĩ tranh luận nên theo định dạng gì → tập trung 100% vào logic.
    - **ESLint - Cảnh báo lỗi code và formatting issues:**
        - **Vai trò:** Phát hiện lỗi sai định dạng tiềm ẩn (unused variables, missing return, etc.) và vi phạm tiêu chuẩn coding.
        - **Ví dụ:** Cảnh báo khi bạn không dùng `===` thay vì `==`, hoặc khai báo biến không dùng.
        - **Khi nào dùng:** Luôn luôn - nó giúp bắt bug sớm và bắt mọi người tuân theo quy tắc team.
    - **Prettier - Auto-format code theo chuẩn:**
        - **Vai trò:** Tự động định dạng lại code (indent, dòng trống, vị trí ngoặc, etc.) mỗi khi save file.
        - **Ví dụ:** Bạn viết code thế nào cũng được, Prettier sẽ tự sửa thành chuẩn chung khi save.
        - **Khi nào dùng:** Dùng cùng ESLint để tự động hoá 100% formatting, team không phải tranh luận.

### Kết clip

- **Tóm tắt:** Formatting không chỉ để đẹp; nó giúp tránh đọc sai, hiểu sai và sửa sai.
- **Viễn cảnh thành công:** Khi sự cố gấp xảy ra, team nhìn code là hiểu luồng ngay, fix đúng ngay lần đầu.
- **Cầu nối sang clip sau:** Khi định dạng đã rõ ràng, bước tiếp theo là dùng comment thế nào cho đúng.