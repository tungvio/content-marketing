Trang-thai: cho-duyet

# Dàn Ý: Phần Còn Lại - Clean Code (Video Dài)

**Ghi chú:** Đây là dàn ý cho phần Clip_04 đến Clip_07 và phần kết luận của video Clean Code.

---

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

**Mục tiêu của phần này:** Hiểu formatting là một phần của Clean Code để giảm đọc sai, hiểu sai, debug sai.

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

---

## **Folder: Clip_05**

## 5. Comments (Bình luận): Khi nào cần, khi nào thừa?

### Vấn đề ngoại tại (Tình huống)

**Thái cực A: Quá ít comment**
```javascript
function processOrder(o, i, d) {
  const x = o.items.reduce((a, b) => a + b.price * b.qty, 0);
  const y = x * (1 - (o.isMember ? 0.1 : 0));
  if (y > d) return null;
  return { ...o, total: y };
}
```
Nhìn code chẳng hiểu gì cả, "x", "y" là cái gì? Tại sao lại * (1 - ...)?

**Thái cực B: Quá nhiều comment**
```javascript
// Hàm xử lý đơn hàng
function processOrder(order, discount, maxBudget) {
  // Tính tổng giá
  const total = order.items.reduce((sum, item) => sum + item.price * item.qty, 0);
  // Kiểm tra xem có phải thành viên không
  // Nếu là thành viên thì giảm giá 10%
  // Tính giá sau giảm
  const finalPrice = total * (1 - (order.isMember ? 0.1 : 0));
  // Kiểm tra xem giá có vượt ngân sách không
  if (finalPrice > maxBudget) return null;
  // Trả về đơn hàng đã xử lý
  return { ...order, total: finalPrice };
}
```
Comment quá dài, dễ bị bỏ đi khi sửa code, **code sẽ tự nói nếu viết tốt.**

### Vấn đề nội tại (Cảm xúc)

**Niềm tin sai lệch:**
- "Code mà cần comment thì code viết tệ" (Clean Code quá tuyệt đối)
- "Phải comment mọi thứ để người khác hiểu" (Comment quá tràn lan)
- "Comment là công việc phụ, không quan trọng" (Bỏ qua comment hoàn toàn)

### Giải pháp (Solution)

**Quy tắc vàng:** **Good code > No comment. But good code + good comment > just good code**

**Khi NÊN comment:**

1. **TÍNH VĂN HÓA, LOGIC PHỨC TẠP**
```javascript
// Thuật toán Sieve of Eratosthenes
// Time: O(n log log n), Space: O(n)
// Không sử dụng modulo vì quá chậm, thay vào đó kiểm tra bằng flag array
const sieve = (n) => {
  const isPrime = Array(n + 1).fill(true);
  isPrime[0] = isPrime[1] = false;
  for (let i = 2; i * i <= n; i++) {
    if (isPrime[i]) {
      for (let j = i * i; j <= n; j += i) {
        isPrime[j] = false;
      }
    }
  }
  return isPrime;
};
```

2. **CẢNH BÁO NGUY HIỂM**
```javascript
// ⚠️ DON'T: Không sửa thứ tự các trường này
// vì database migration đã quyết định order này
const fields = ['id', 'createdAt', 'email', 'name'];

// ⚠️ BUG KNOWN: API response của third-party đôi khi không có 'phone' field
// Trả về '0' thay vì null là *workaround* tạm thời
const phone = response.phone || '0';
```

3. **INPUT/OUTPUT, SIDE EFFECTS**
```javascript
// Tính toán heavy operation - mất ~500ms
// Kết quả được cache trong 1 giờ
const getReportMetrics = memoize(
  async (userId) => { ... },
  { ttl: 3600000 }
);
```

4. **TẠI SAO KHÔNG DÙNG CÁCH HIỀU NHÂN**
```javascript
// ❌ WRONG: Không dùng optional chaining ở đây
// vì backend của chúng ta luôn trả về user?.profile?.avatar
// Dùng ! để catch lỗi sớm hơn nếu backend sai
const avatar = user!.profile!.avatar;
```

**Khi KHÔNG nên comment:**

1. **Code đã nói cho mình nghe**
```javascript
// ❌ KHÔNG CẦN
// Lặp qua các users
users.forEach(user => {
  // Gửi email tới user
  sendEmail(user.email);
});

// ✅ TỐTCÓ
users.forEach(user => sendEmail(user.email));
```

2. **Comment là "bản sao" của code**
```javascript
// ❌ KHÔNG CẦN
// Kiểm tra xem tuổi có >= 18 không
if (age >= 18) {
  // Là người lớn
  return true;
}

// ✅ TỐT
const isAdult = age >= 18;
if (isAdult) return true;
```

3. **Giải thích một biến tên xấu thay vì đổi tên**
```javascript
// ❌ KHÔNG NÊN
const u = userService.getById(id); // u là user

// ✅ TỐT
const user = userService.getById(id);
```

**Chiến lược comment:**
- **Dòng trên logic lạ, phức tạp, counterintuitive → Comment**
- **Dòng trên logic rõ ràng, đơn giản → Không comment**
- **Dòng có side effect hay risk → Comment ⚠️**

---

## **Folder: Clip_06**

## 6. Những lầm tưởng về Clean Code

### Vấn đề nội tại (Cảm xúc)

**Bạn có thể nghĩ:**
- "Clean Code khó quá, tôi không đủ level"
- "Clean Code là luxury, khi nào có thời gian thì làm"
- "Clean Code chỉ cần cho big tech, mình làm pet project không cần"

**Đó là LẦMTƯỞNG đôi khi gây phản tác dụng:**

### Giải pháp (Làm rõ 5 lầm tưởng phổ biến)

**Lầm tưởng #1: "Càng ít dòng code, càng clean"**
```javascript
// ❌ KHÔNG
const p = (arr, fn) => arr.reduce((a, b) => a + fn(b), 0);
const t = p(orders, o => o.items.reduce((a, i) => a + i.price * i.qty, 0));

// ✅ CÓ
const sumByProperty = (arr, fn) => arr.reduce((sum, item) => sum + fn(item), 0);
const calculateTotalRevenue = (orders) => {
  return sumByProperty(orders, order => calculateOrderAmount(order));
};
```
**Clean Code ≠ Code ngắn. Clean Code = Code rõ ràng dù có thể dài hơn.**

**Lầm tưởng #2: "Comment nhiều = Code clean"**
- Comment không phải thay thế cho code tốt.
- Nếu cần comment để giải thích logic đơn giản, **code viết tệ.**
- Comment **bổ sung**, không **thay thế** code rõ ràng.

**Lầm tưởng #3: "Clean Code = Không có bug"**
- Clean Code giúp **phát hiện bug nhanh hơn, fix dễ hơn.**
- Code tệ có bug → khó debug, mất vài giờ.
- Code sạch có bug → dễ tìm, 10 phút fix xong.

**Lầm tưởng #4: "Mãi mãi dùng design patterns chuyên nghiệp"**
```javascript
// ❌ QUÁĐỘ
class AbstractFactoryBuilderPatternValidator {
  private delegators: Map<...>;
  async validateUsingStrategyPattern() { ... }
}

// ✅ VỪA ĐÚNG
function validateOrder(order) {
  if (!order.items.length) throw new Error('Order cannot be empty');
  if (order.total < 0) throw new Error('Invalid total');
  return true;
}
```
**Đừng "thiết kế quá mức" cho một bài toán đơn giản.**

**Lầm tưởng #5: "Refactor = Đập đi xây lại"**
- Refactor **đơn giản từng bước nhỏ**, không cô lập thay đổi lớn.
- Sau mỗi bước refactor, phải test lại.
- Safe refactor = Có unit test bao phủ trước.

---

## **Folder: Clip_07**

## 7. Balance giữa Clean Code và Deadline

### Vấn đề ngoại tại (Tình huống)

**Hiện trạng 1: Đẩy mạnh deadline, bỏ clean code**
```javascript
// ❌ Monday: Code vội vàng
function doStuff(data) {
  let x = 0;
  for (let i = 0; i < data.length; i++) {
    if (data[i].status === 'active' && data[i].value > 100) {
      x += data[i].amount;
    }
  }
  return x;
}

// ❓ Thursday: "Tại sao chẳng ai hiểu cái hàm này?"
// ❌ Next week: "Phải sửa logic nhưng sợ break cái khác"
```

**Hiện trạng 2: "Refactor mãi không bao giờ xong"**
- Sếp: "Tính năng mới đâu?"
- Bạn: "Đang refactor code cũ..."
- Sếp: "Khách hàng không care refactor, họ chỉ care feature mới!"

**Khó khăn:**
- Deadline gấp → Viết code vội → Code bẩn → Sau này sửa lâu hơn
- Có thời gian → Muốn clean code → Refactor quá → Không kịp deadline

### Vấn đề nội tại (Cảm xúc)

**Xung đột nội tâm:**
- "Tôi lại viết code bẩn"
- "Tôi là developer tệ"
- "Công ty chỉ care deadline, không care quality"

### Giải pháp (Solution)

**Chiến lược: Cân bằng thông minh**

**Giai đoạn 1: MVP (Tuần 1)**
```
Mục tiêu: Chạy được, có feature
Bỏ qua: Refactor chi tiết, edge cases
Làm: Tên function rõ ràng, code dễ hiểu (tối thiểu)
```

**Giai đoạn 2: Stabilize (Tuần 2-3)**
```
Mục tiêu: Code sạch, refactor từng phần
Bỏ qua: Thêm feature mới
Làm: Tách function, xóa duplication, test
```

**Giai đoạn 3: Feature Addition (Tuần 4+)**
```
Mục tiêu: Thêm feature mới, maintain code quality
Bỏ qua: Hoàn hảo 100%
Làm: Balance giữa feature và quality
```

**Quy tắc thực tế:**

1. **"Boy Scout Rule"** - Mỗi khi sửa, để code sạch hơn trước đó
   - Đừng refactor toàn bộ file
   - Chỉ sạch hóa phần bạn sửa

2. **SOLID cơ bản** - Không cần 100%, nhưng nên có 70%
   - Single Responsibility: Hàm chỉ làm 1 việc
   - Dependency Injection: Truyền vào thay vì hardcode

3. **Test đủ để yên tâm** - Không cần 100% coverage
   - Test business logic chính
   - Test edge cases quan trọng
   - Bỏ test trivial (getter, setter)

4. **Deadline 1 tuần?**
   - Viết code chạy được
   - Tối thiểu: tên biến, tên hàm phải rõ ràng
   - Tối thiểu: không duplicate code quá 3 chỗ

   **Deadline 1 tháng?**
   - Áp dụng đầy đủ 3 kỹ thuật: Naming, Extract Function, Formatting
   - Viết test cho core logic
   - Không cần refactor chi tiết

---

## **Phần Kết Luận**

### Folder: Clip_08 - Viễn Cảnh Thành Công

**Nếu bạn áp dụng Clean Code:**

**Scenario A: 3 tháng sau**
- Code cũ đọc lại dễ dàng, không mất cả ngày để hiểu
- Sửa bug nhanh hơn, không sợ lado effect
- Review PR nhanh hơn, team hạnh phúc hơn

**Scenario B: 1 năm sau**
- Code base dễ bảo trì, có giá trị cao
- Onboard junior dev nhanh hơn
- Giữ được tốc độ phát triển tính năng, không bị chậm dần

**Scenario C: Xin việc mới**
- Portfolio có clean code → Ấn tượng với hiring manager
- Phỏng vấn: Code được hỏi → Explain rõ logic → Pass dễ
- Lương cao hơn vì "chất lượng code" là yếu tố


### Folder: Clip_09 - Tóm Lại & Lời Khuyên Cuối

**3 điều nhớ lâu:**

1. **Naming tốt = 50% Clean Code** - Đặt tên rõ ràng là bước đầu tiên
2. **Extract function = Dễ bảo trì** - Tách logic trùng lặp, code dễ thay đổi
3. **Formatting consistent = Team hạnh phúc** - Chuẩn hoá formatting tiết kiệm giờ

**5 bước NGAY HÔM NAY:**

1. Ở project hiện tại, tìm 3 hàm có tên tệ → Đổi tên
2. Tìm 1 đoạn code lặp lại 3+ lần → Tách thành hàm riêng
3. Install Prettier + ESLint → Tự động format
4. Viết comment cho 1 logic phức tạp (nếu có)
5. Refactor 1 function tệ nhất theo 3 nguyên tắc

---

**END OF OUTLINE FOR PART 2**

---

## Ghi Chú cho Content Writer:

1. **Tone:** Vẫn giữ tone casual, gần gũi, không lười.
2. **Ví dụ code:** Cần cụ thể, dễ hiểu, tránh trivial.
3. **Thẩm phát vấn đệ:** Problem, Agitate, Solution (PAS) logic vẫn giữ.
4. **Kết thúc:** Nên có CTA rõ ràng (5 bước ngay hôm nay).
5. **Animation/Visual:** Cần ghi chú lại các animation cần cho Clip nếu có.
