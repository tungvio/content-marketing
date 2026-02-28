# Giáo Án

---

# Kỹ Thuật Nêu Vấn Đề: **Công Thức P-A**

## 1. Mục Tiêu

- **Tạo ra sự đồng cảm:** Hiểu rằng trước khi đưa ra một giải pháp, cần phải làm cho người học hiểu rõ "nỗi đau" của vấn đề một cách thuyết phục.
- **Áp dụng công thức P-A (Problem - Analysis):** Biết cách trình bày một đoạn code có vấn đề (Problem) và sau đó phân tích một cách logic tại sao nó chưa tối ưu (Analysis).
- **Học cách phân tích tác hại:** Không chỉ nói "code này chưa tốt", mà còn phải chỉ ra được những hậu quả cụ thể của nó đối với logic, hiệu năng và khả năng bảo trì.
- **Biết cách sử dụng ví dụ so sánh (ẩn dụ):** Học cách dùng các hình ảnh đời thường để giải thích các vấn đề kỹ thuật phức tạp, giúp người học dễ hình dung và ghi nhớ.

## 2. Nội dung

### 2.1 Tư duy cốt lõi: Vấn Đề Càng Rõ Ràng, Giải Pháp Càng Giá Trị

- **Định nghĩa:** Kỹ thuật nêu vấn đề là bước đầu tiên và quan trọng nhất trong việc giảng dạy hay trình bày một kiến thức mới. Thay vì vội vàng đưa ra giải pháp, bạn cần dành thời gian để chỉ rõ vấn đề đang tồn tại, nó gây ra những bất tiện và tác hại như thế nào.
- **Khi nào nên áp dụng?** Bạn nên áp dụng kỹ thuật nêu vấn đề trong **bất kỳ tình huống nào** mà bạn cần thuyết phục người khác **trước khi** giải quyết một vấn đề nào đó.
- **Sự khác biệt:**
    - **❌ Cách tiếp cận kém hiệu quả:** Nhảy thẳng vào phần giới thiệu giải pháp.
        - *"Hôm nay chúng ta sẽ học về Promise, nó giúp xử lý bất đồng bộ."*
        - **Vấn đề:** Người học sẽ cảm thấy mơ hồ. Họ chưa nhận thấy sự cần thiết, không biết Promise ra đời để giải quyết vấn đề cụ thể nào, nên sẽ khó tiếp thu và ghi nhớ.
    - **✅ Cách tiếp cận hiệu quả:** Bắt đầu bằng việc cho thấy vấn đề trong thực tế.
        - *"Hãy cùng xem đoạn code xử lý nhiều tác vụ bất đồng bộ lồng nhau này. Các bạn có nhận ra cấu trúc phức tạp lồng nhau…(giải thích cụ thể)"*
        - **Kết quả:** Người học nhìn thấy ngay một cấu trúc rắc rối, cảm nhận được sự khó khăn của người viết code, và bắt đầu tò mò: "Làm thế nào để cải thiện điều này?". Lúc này, họ đã hoàn toàn sẵn sàng để đón nhận giải pháp.
- **💡 Tư duy đúng đắn:** Luôn tự hỏi: *"Làm thế nào để người đọc nhìn vào đoạn code, nghe mình nói; rồi có thể tự nhận ra vấn đề một cách dễ dàng?"*

### 2.2 Kỹ thuật thực tế: Áp dụng công thức P-A

Đây là công thức 2 bước đơn giản để trình bày vấn đề. Chúng ta sẽ lấy ví dụ về cách truyền tham số cho hàm trong JavaScript.

- **Bước 1: Problem (Trình Bày Vấn Đề)**
    - **Hành động:** Hãy trình bày đoạn code có vấn đề trước tiên. Đừng giải thích gì vội. Mục tiêu giúp người xem hiểu nhanh được bối cảnh hiện tại là gì.
    - **Ví dụ:**
        - ***Script:** "Như bạn thấy, đây là hàm có tên là `createProduct` dùng để tạo sản phẩm mới. Hàm này nhận vào một object chứa thông tin sản phẩm:*
            
            ```jsx
            // BEFORE (Đây là code CHƯA TỐI ƯU)
            
            function createProduct(product) {
              // Bên trong hàm, chúng ta phải truy cập từng thuộc tính
              const name = product.name;
              const price = product.price;
              const category = product.category;
              const inStock = product.inStock;
            
              console.log(`Tên: ${name}, Giá: ${price}, Danh mục: ${category}, Tình trạng: ${inStock}`);
              // ... logic tạo sản phẩm ...
            }
            
            // Cách gọi hàm
            const newProduct = {
              name: 'iPhone 15',
              price: 1000,
              category: 'Electronics',
              inStock: true
            };
            
            createProduct(newProduct);
            ```
            
- **Bước 2: Analysis (Phân Tích Tại Sao Nó Chưa Tối Ưu)**
    - **Hành động:** Bây giờ, hãy giải thích tại sao cách viết trên tuy chạy được nhưng lại có nhiều nhược điểm.
    - **Ví dụ:**
        - ***Script:** "Đoạn code trên hoạt động đúng, không có lỗi. Tuy nhiên, nó có một vài nhược điểm:*
            1. ***Thừa thãi và dài dòng:** Bên trong hàm, chúng ta phải lặp lại `product.` để truy cập từng thuộc tính. Nếu object có nhiều thuộc tính, việc khai báo biến sẽ rất tốn công.*
            2. ***Chữ ký hàm không rõ ràng:** Khi nhìn vào `function createProduct(product)`, chúng ta không biết object `product` cần chứa những thuộc tính cụ thể nào. Chúng ta phải đọc toàn bộ code bên trong hàm mới có thể hiểu được.*
            3. ***Dễ gây lỗi tiềm ẩn:** Nếu gõ nhầm `product.nane` thay vì `product.name`, JavaScript sẽ không báo lỗi. Nó chỉ trả về giá trị `undefined`, khiến việc tìm và sửa lỗi trở nên khó khăn hơn.*
        - ***Dùng ví dụ so sánh (Tùy chọn):*** *Nó giống như việc bạn nhận được một **hộp quà không có nhãn**. Bạn phải mở hoàn toàn chiếc hộp và xem xét từng món đồ thì mới biết bên trong có gì. Cách làm này không hiệu quả và tốn thời gian."*

### 2.3 Nghệ thuật Phân Tích (Analysis)

Để phần phân tích sâu sắc hơn, hãy xem xét vấn đề từ nhiều góc độ:

- **Tác hại về Logic:** Nó có thể gây ra những lỗi nào? (Ví dụ: Trả về giá trị không mong muốn, thứ tự thực thi sai...).
- **Tác hại đối với Lập trình viên:** Nó ảnh hưởng thế nào đến người làm việc với code? (Ví dụ: Khó đọc, gây khó khăn khi sửa lỗi, tạo ra rào cản cho thành viên mới...).
- **Tác hại về Lâu dài (Bảo trì):** Nó ảnh hưởng thế nào đến dự án trong tương lai? (Ví dụ: Tạo ra nợ kỹ thuật (technical debt), khó khăn khi thêm tính năng mới hoặc mở rộng...).

**📌 Lưu ý:**

- **Vấn đề càng rõ ràng, giải pháp càng có giá trị.** Hãy đầu tư thời gian vào bước nêu vấn đề, giải pháp của bạn sẽ được đón nhận một cách tích cực hơn.
- Luôn bắt đầu bằng sự đồng cảm. Cho người đọc thấy bạn hiểu những khó khăn họ có thể gặp phải.
- Việc trình bày trực quan một đoạn code chưa tối ưu và chỉ ra từng vấn đề sẽ có tác động rất mạnh.
- **👉 Làm bài tập:** [Bài Tập](B%C3%A0i%20T%E1%BA%ADp%202ccb9e967cbc805c8bf4c388d3bc02b2.md)

---

# Kỹ Thuật Trình Bày Code Từng Bước: Hướng Dẫn Code Một Cách Dễ Hiểu

## 1. Mục Tiêu

- Chuyển suy nghĩ từ việc "chỉ đưa ra code" sang "dẫn dắt qua từng dòng code".
- **Hiểu và áp dụng thành thạo công thức P-C-E-E (Purpose - Code - Explain - Expand)** để tạo ra các video hướng dẫn hoặc bài blog về code cực kỳ dễ theo dõi.
- Biết cách giải thích rõ ràng **"tại sao"** đằng sau mỗi dòng code, chứ không chỉ dừng lại ở việc **"nó là gì"**.
- Tạo ra nội dung hướng dẫn code mà người mới bắt đầu cũng có thể làm theo, hiểu sâu và cảm thấy tự tin.

## 2. Nội dung

### 2.1 Tư duy cốt lõi: Đừng Đưa Code, Hãy Dẫn Dắt

- **Định nghĩa:** Kỹ thuật này áp dụng nguyên tắc **"Viết Như Đang Dạy Học"** vào việc hướng dẫn lập trình. Thay vì chỉ dán một khối code lớn và giải thích chung chung, bạn sẽ chia nhỏ quá trình, xây dựng code từng dòng một và giải thích ngay lập tức.
- **Sự khác biệt:**
    - **❌ Người trình bày kém hiệu quả:**
        - *"Đây là code để validate form, các bạn sao chép và dán vào nhé."*
        - **Vấn đề:** Người học không hiểu được tư duy đằng sau. Họ chỉ có thể sao chép một cách máy móc và sẽ không thể tự làm lại trong một tình huống khác.
    - **✅ Người hướng dẫn hiệu quả:**
        - *"Được rồi, bây giờ chúng ta sẽ bắt đầu kiểm tra cho trường `name`. Để làm điều đó, đầu tiên chúng ta cần một công cụ từ thư viện..."*
        - **Kết quả:** Người học được dẫn dắt qua từng bước suy nghĩ, hiểu rõ mục đích của từng dòng code. Họ không chỉ biết **cách làm**, mà còn hiểu **tại sao phải làm như vậy**.
- **So sánh dễ hiểu:**
    - Cách làm kém hiệu quả giống như đưa cho du khách một tấm bản đồ và nói "Tự đi đi".
    - Cách làm tốt giống như một hướng dẫn viên du lịch đi cùng, chỉ vào từng điểm và giải thích ý nghĩa của nó trên đường đi.

### 2.2 Công Thức P-C-E-E

Đây là công thức 4 bước đơn giản để cấu trúc phần trình bày code của bạn.

- **Purpose (Nêu Mục Đích)**
    - **Hành động:** Nêu rõ mục tiêu của đoạn code bạn **sắp viết**. Cho người học biết rõ mục đích hành động sắp đến là gì.
    - **Ví dụ Script:**
        - *Thoại: Bây giờ, mình sẽ cài đặt thư viện `express-validator` vào bên trong dự án.*
- **Code (Viết Code)**
    - **Hành động:** Gõ hoặc hiển thị **chỉ duy nhất** đoạn code cần thiết để hoàn thành mục tiêu đã nêu ở bước Purpose.
    - **Ví dụ Script:**
        - *Thoại (Tùy chọn): Để cài đặt thư viện, mình sẽ mở terminal và gõ lệnh sau:*
            
            ```bash
            npm install express-validator
            ```
            
- **Explain (Giải Thích)**
    - **Hành động:** Giải thích ngay lập tức đoạn code bạn vừa gõ. Nó làm gì? Từng phần có ý nghĩa gì?
    - **Ví dụ Script:**
        - *Thoại: Lệnh này sẽ giúp tải thư viện `express-validator` từ trên mạng về và cài vào dự án. Sau khi lệnh này chạy xong, mình có thể bắt đầu sử dụng thư viện này trong mã nguồn.*
- **Expand (Mở Rộng Thêm)**
    - **Hành động:** Cung cấp thêm kinh nghiệm cá nhân, thông tin, bối cảnh, hoặc các lựa chọn khác liên quan đến đoạn code vừa viết. Đây là bước tạo ra giá trị khác biệt.
    - **Ví dụ Script:**
        - *Thoại: Một mẹo nhỏ là các bạn có thể dùng lệnh `npm i` thay cho `npm install`, tại vì nó ngắn gọn hơn nhưng có chức năng tương tự.*

### 2.3 Sự Linh Hoạt: Không Phải Lúc Nào Cũng Cần Đủ 4 Bước

- **📌 Lưu ý:** Điều quan trọng cần nhớ là P-C-E-E là một **khung sườn**, không phải là một **khuôn mẫu cứng nhắc**. Tùy vào đối tượng người xem, độ phức tạp của code và nhịp độ bài giảng, bạn hoàn toàn có thể lược bỏ hoặc gộp các bước để giữ cho nội dung trôi chảy và tự nhiên.
- **👉 Nguyên tắc chung:** Cái gì quá đơn giản hoặc lặp lại, càng có thể lược bỏ.
- **Lược bỏ "Expand" (Mở rộng)**
    
    Đây là bước dễ được lược bỏ nhất để giữ cho bài giảng tập trung.
    
    - **Khi nào nên lược bỏ?**
        - Khi đoạn code cực kỳ đơn giản, không có nhiều thứ để nói thêm.
        - Khi bạn đang ở giữa một chuỗi hành động dài liên tiếp và không muốn làm gián đoạn dòng chảy bằng những thông tin bên lề.
    - **Ví dụ:**
        - **Ngữ cảnh:** Bạn đang hướng dẫn cách khai báo các biến cơ bản trong JavaScript.
        - **Purpose:** *Đầu tiên, chúng ta sẽ khai báo một biến `age` để lưu tuổi và gán cho nó giá trị là `25`.*
        - **Code:**
            
            ```bash
            let age = 25;
            ```
            
        - **Explain:** *Ở đây, `let` là từ khóa để khai báo biến, `age` là tên biến, và `25` là giá trị mình gán cho nó.*
        - **→ Bỏ qua "Expand":** Đoạn code này quá cơ bản.
- **Lược bỏ "Explain" (Giải thích)**
    
    Bước này ít khi được lược bỏ, nhưng rất hiệu quả để tăng tốc độ khi một mẫu kiến thức đã trở nên quen thuộc.
    
    - **Khi nào nên lược bỏ?**
        - Khi đoạn code lặp lại một mẫu kiến thức mà bạn vừa giải thích ngay trước đó.
        - Khi đoạn code rất đơn giản, hoặc quá quen thuộc với **đối tượng người xem hiện tại**.
    - **Ví dụ:**
        - **Ngữ cảnh:** Ngay sau ví dụ về biến `age` ở trên.
        - **Purpose:** ”*Tương tự, bây giờ mình sẽ khai báo một biến `name` để lưu tên.”*
        - **Code:**
            
            ```bash
            let name = "John";
            ```
            
        - **→ Bỏ qua "Explain":** Người học đã được giải thích về `let`, tên biến và giá trị. Không cần giải thích lại.

### 2.4 Vòng lặp P-C-E-E

Bây giờ, bạn hãy cùng xem cách công thức **P-C-E-E** được áp dụng liên tiếp, **lúc đầy đủ**, **lúc lược bỏ**, để xây dựng một đoạn script hướng dẫn hoàn chỉnh:

- **Vòng lặp 1: Tạo cấu trúc hàm async - Đầy đủ 4 bước**
    - **1. Purpose (Nêu Mục Đích):**
        - **Script:** *"Okay, mục tiêu của chúng ta bây giờ là viết một hàm để lấy danh sách người dùng từ một API. Vì đây là một tác vụ bất đồng bộ, chúng ta sẽ sử dụng cú pháp `async/await`. Đầu tiên, hãy tạo ra cấu trúc cơ bản của một hàm `async`.*
    - **2. Code (Viết Code):**
        - **Script:** *Mình sẽ định nghĩa một hàm tên là `fetchUsers` như sau:*
            
            ```jsx
            async function fetchUsers() {
            
            }
            ```
            
    - **3. Explain (Giải Thích):**
        - **Script:** *Từ khóa `async` đặt trước function có ý nghĩa rất quan trọng. Nó báo cho JavaScript biết rằng 'hàm này sẽ chứa những tác vụ bất đồng bộ bên trong'. Điều này cho phép mình sử dụng từ khóa `await` ở các bước tiếp theo.*
    - **4. Expand (Mở Rộng Thêm):**
        - **Script:** *Ngoài cách viết `async function`, các bạn cũng có thể định nghĩa một `arrow function async`, trông sẽ như thế này: `const fetchUsers = async () => {}`. Cả hai cách đều có tác dụng như nhau, tùy vào sở thích của bạn.*
- **Vòng lặp 2: Gọi API bằng `fetch` và `await` - Đầy đủ 4 bước**
    - **1. Purpose (Nêu Mục Đích):**
        - **Script:** *Bước tiếp theo, mình cần thực hiện việc gọi đến API để lấy dữ liệu về.*
    - **2. Code (Viết Code):**
        - **Script:** *Mình sẽ sử dụng hàm `fetch` có sẵn của trình duyệt và thêm từ khóa `await` ở phía trước:*
            
            ```diff
            async function fetchUsers() {
            + const response = await fetch('https://jsonplaceholder.typicode.com/users');
            }
            ```
            
    - **3. Explain (Giải Thích):**
        - **Script:** *Ở đây có 2 phần quan trọng. `fetch(...)` là hàm để gửi yêu cầu đến URL được cung cấp. Từ khóa `await` đứng trước nó sẽ yêu cầu chương trình 'dừng lại và chờ' cho đến khi yêu cầu này hoàn thành và nhận được phản hồi (response) từ server. Sau khi có phản hồi, nó sẽ được gán vào biến `response`.*
    - **4. Expand (Mở Rộng Thêm):**
        - **Script:** *Nếu không có `await`, chương trình sẽ không chờ mà chạy tiếp ngay lập tức, và biến `response` sẽ không nhận được dữ liệu mong muốn. Đây chính là sức mạnh của `async/await`: nó giúp chúng ta viết code bất đồng bộ trông giống như code đồng bộ, rất dễ đọc.*
- **Vòng lặp 3: Xử lý dữ liệu JSON - Lược bỏ "Expand"**
    - **1. Purpose (Nêu Mục Đích):**
        - **Script:** *Phản hồi mà server trả về chưa phải là dữ liệu mình dùng được ngay. Bây giờ, mình cần chuyển đổi phản hồi đó thành một đối tượng JavaScript mà mình có thể sử dụng.*
    - **2. Code (Viết Code):**
        - **Script:** *Mình thêm một dòng code như sau:*
            
            ```diff
            async function fetchUsers() {
              const response = await fetch('https://jsonplaceholder.typicode.com/users');
            + const users = await response.json();
            }
            ```
            
    - **3. Explain (Giải Thích):**
        - **Script:** *Phương thức `.json()` của đối tượng `response` cũng là một tác vụ bất đồng bộ, vì nó cần thời gian để đọc và phân tích dữ liệu. Do đó, chúng ta cũng phải dùng `await` để 'chờ' cho quá trình này hoàn tất. Sau khi xong, dữ liệu người dùng thực sự sẽ được gán vào biến `users`.*
    - **→ Bỏ qua "Expand":** Tại vì muốn người xem tập trung vào việc lấy được dữ liệu.
- **Vòng lặp 4: In kết quả ra console - Lược bỏ "Explain" và "Expand"**
    - **1. Purpose (Nêu Mục Đích):**
        - **Script:** *Cuối cùng, mình in kết quả ra console để kiểm tra xem đã lấy được dữ liệu thành công hay chưa.*
    - **2. Code (Viết Code):**
        
        ```diff
        async function fetchUsers() {
          const response = await fetch('https://jsonplaceholder.typicode.com/users');
        	const users = await response.json();
        + console.log(users);
        }
        ```
        
    - **→ Bỏ qua "Explain" và "Expand":** Đối với các lập trình viên, `console.log` là một hàm quá quen thuộc. Việc giải thích lại "đây là hàm để in ra console" là không cần thiết.
- **👉 Script cuối cùng:**
    
    *Okay, mục tiêu của chúng ta bây giờ là viết một hàm để lấy danh sách người dùng từ một API.*
    
    *Vì đây là một tác vụ bất đồng bộ, chúng ta sẽ sử dụng cú pháp `async/await`. Đầu tiên, hãy tạo ra cấu trúc cơ bản của một hàm `async`.*
    
    *Mình sẽ định nghĩa một hàm tên là `fetchUsers` như sau:*
    
    ```jsx
    async function fetchUsers() {
    
    }
    ```
    
    *Từ khóa `async` đặt trước function có ý nghĩa rất quan trọng. Nó báo cho JavaScript biết rằng 'hàm này sẽ chứa những tác vụ bất đồng bộ bên trong'.*
    
    *Điều này cho phép mình sử dụng từ khóa `await` ở các bước tiếp theo.*
    
    *Bước tiếp theo, mình cần thực hiện việc gọi đến API để lấy dữ liệu về.*
    
    *Mình sẽ sử dụng hàm `fetch` có sẵn của trình duyệt và thêm từ khóa `await` ở phía trước:*
    
    ```diff
    async function fetchUsers() {
    +  const response = await fetch('https://jsonplaceholder.typicode.com/users');
    }
    ```
    
    *Ở đây có 2 phần quan trọng:*
    
    - `*fetch(...)` là hàm để gửi yêu cầu đến URL được cung cấp.*
    - *Từ khóa `await` đứng trước nó sẽ yêu cầu chương trình 'dừng lại và chờ' cho đến khi yêu cầu này hoàn thành và nhận được phản hồi (response) từ server.*
    
    *Sau khi có phản hồi, nó sẽ được gán vào biến `response`.*
    
    *Nếu không có `await`, chương trình sẽ không chờ mà chạy tiếp ngay lập tức, và biến `response` sẽ không nhận được dữ liệu mong muốn.*
    
    *Đây chính là sức mạnh của `async/await`: Nó giúp chúng ta viết code bất đồng bộ trông giống như code đồng bộ, rất dễ đọc.*
    
    *Phản hồi mà server trả về chưa phải là dữ liệu mình dùng được ngay. Bây giờ, mình cần chuyển đổi phản hồi đó thành một đối tượng JavaScript mà mình có thể sử dụng.*
    
    *Mình thêm một dòng code như sau:*
    
    ```diff
    async function fetchUsers() {
      const response = await fetch('https://jsonplaceholder.typicode.com/users');
    + const users = await response.json();
    }
    ```
    
    *Phương thức `.json()` của đối tượng `response` cũng là một tác vụ bất đồng bộ, vì nó cần thời gian để đọc và phân tích dữ liệu.*
    
    *Do đó, chúng ta cũng phải dùng `await` để 'chờ' cho quá trình này hoàn tất. Sau khi xong, dữ liệu người dùng thực sự sẽ được gán vào biến `users`.*
    
    *Cuối cùng, mình in kết quả ra console để kiểm tra xem đã lấy được dữ liệu thành công hay chưa.*
    
    ```diff
    async function fetchUsers() {
      const response = await fetch('https://jsonplaceholder.typicode.com/users');
      const users = await response.json();
    + console.log(users);
    }
    ```
    

**📌 Lưu ý:**

- **P-C-E-E là một vòng lặp.** Bạn sẽ lặp lại chu trình này cho mỗi đoạn code nhỏ mà bạn giới thiệu.
- Mục tiêu cuối cùng là sau khi xem xong, người học không chỉ có một đoạn code chạy được, mà còn **hoàn toàn tự tin** về những gì họ vừa viết.
- **👉 Làm bài tập:** [Bài Tập](B%C3%A0i%20T%E1%BA%ADp%202ccb9e967cbc805c8bf4c388d3bc02b2.md)

---

# Làm Chủ Nhịp Độ Hướng Dẫn

## 1. Mục Tiêu

- Nâng cao kỹ năng áp dụng P-C-E-E từ mức "biết dùng" lên "dùng linh hoạt".
- **Hiểu và vận dụng nguyên tắc cốt lõi:** **"Cái gì LẠ thì CHI TIẾT, cái gì QUEN thì GOM LẠI"**.
- Tạo ra các video hướng dẫn hoặc bài viết có nhịp độ hợp lý, lúc chậm rãi chi tiết, lúc nhanh gọn hiệu quả, giúp người học không bị nhàm chán và luôn tập trung.

## 2. Nội dung

### 2.1 Tư duy cốt lõi: Đừng Dạy Mọi Thứ Như Nhau

- **Vấn đề của việc áp dụng máy móc:** Trong một số trường hợp. nếu chúng ta áp dụng P-C-E-E cho **mọi dòng code** một cách cứng nhắc, bài hướng dẫn sẽ trở nên rất chậm, dài dòng và đôi khi nhàm chán, đặc biệt là với những đoạn code lặp lại.
- **👉 Nguyên tắc:** Cái gì LẠ thì CHI TIẾT, cái gì QUEN thì GOM LẠI
- **Giải thích:**
    - **Cái gì LẠ:** Là những khái niệm, cú pháp, hoặc công nghệ mới mà bạn chưa đề cập cho người xem trước đó. Với những kiến thức này, bạn cần đi thật chậm, đi vào từng chi tiết nhỏ.
    - **Cái gì QUEN:** Là những **mẫu logic lặp lại** mà bạn đã giải thích cho người xem ngay trước đó, hoặc **những kiến thức quá quen thuộc** với người xem. Với những nội dung này, chúng ta nên đi nhanh hơn bằng cách gom chúng lại.
- **Mục tiêu:** Tạo ra một nhịp độ hướng dẫn tự nhiên, giống như một cuộc trò chuyện. Chỗ nào cần nhấn mạnh thì nói kỹ, chỗ nào ai cũng biết thì lướt qua nhanh.

### 2.2 Hai cách áp dụng P-C-E-E

Chúng ta sẽ chia cách áp dụng P-C-E-E thành 2 cách để bạn linh hoạt sử dụng:

- **Cách 1: Chi tiết**
    - Đây là cách áp dụng P-C-E-E bạn đã vừa học **ở bài trước đó**. Cách này bạn sẽ giải thích chi tiết lần lượt từng đoạn code một.
    - 90% bạn sẽ sử dụng cách này trong các video hướng dẫn.
- **Cách 2: Gom nhóm**
    - Đây là cách áp dụng P-C-E-E ở mức tổng quan, giúp tăng tốc độ bài giảng.
    - **Định nghĩa:** Gom một cụm code (từ 2-5 dòng) thực hiện **cùng một chức năng tương tự** lại thành một khối, sau đó thực hiện **một vòng lặp P-C-E-E** cho cả khối đó.
    - **Khi nào dùng:** Những mẫu logic lặp lại mà bạn đã giải thích cho người xem ngay trước đó, hoặc những kiến thức quá quen thuộc với người xem.
    - **Ví dụ:**
        - **Bối cảnh:** Trước đó, bạn đã hướng dẫn người xem thiết lập validate cho trường `name`:
            
            ```jsx
            body('name').notEmpty().withMessage('Tên không được để trống.'),
            ```
            
        - **Purpose:** ”*Tương tự trường `name`, bây giờ mình tiến hành validate cho cả `email` và `password`”*
        - **Code - Cả khối:** Gõ (hoặc dán) cả hai dòng code cùng một lúc.
            
            ```diff
            body('name').notEmpty().withMessage('Tên không được để trống.'),
            + body('email').notEmpty().withMessage('Email không được để trống.'),
            + body('password').notEmpty().withMessage('Password không được để trống.')
            ```
            

**📌 Lưu ý:**

- Mục tiêu cuối cùng là tạo ra một trải nghiệm học tập không quá chậm (gây nhàm chán) cũng không quá nhanh (gây khó hiểu).
- **👉 Làm bài tập:** [Bài Tập](B%C3%A0i%20T%E1%BA%ADp%202ccb9e967cbc805c8bf4c388d3bc02b2.md)