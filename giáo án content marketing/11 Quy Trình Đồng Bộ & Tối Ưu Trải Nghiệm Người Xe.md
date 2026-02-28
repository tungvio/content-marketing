# Giáo Án

---

# **Quy Trình Đồng Bộ**

## 1. Mục tiêu

- **Đồng bộ tuyệt đối:** Nắm vững kỹ thuật "Cắm mốc thời gian" để đảm bảo **Lời nói (Audio)** đến đâu, **Hình ảnh (Visual)** xuất hiện chính xác đến đó.
- **Tối ưu quy trình phối hợp:** Xây dựng một "ngôn ngữ chung" thống nhất giữa Content và Editor, giúp loại bỏ hoàn toàn sự phỏng đoán hay hiểu lầm ý đồ.
- **Kiểm soát diễn hoạt (Animation):** Biết cách sử dụng ghi chú (Note) để chỉ định chính xác các hiệu ứng chuyển động phức tạp mà bạn mong muốn Editor thực hiện.

## 2. Nội dung

### 2.1 Bước 1: Xác định thời điểm và cắm mốc thời gian

Đây là bước bạn sẽ chỉ định đến đoạn nào trong kịch bản (Script) thì sẽ hiển thị Frame nào trong Figma.

- **Cách thực hiện:**
    1. **Đừng vội design:** Bạn dự định làm hình ảnh cho 1 câu trong kịch bản. Lúc này, bạn đừng vội lao vào thiết kế ngay. Thay vào đó, bạn suy nghĩ ý tưởng và phác thảo sơ bộ bố cục trước.
    2. **Xác định thời điểm:** Tiếp theo, bạn xác định khi nào sẽ xảy ra một sự kiện chuyển cảnh sang Frame kế tiếp trong câu đó.
    3. **Tạo ghi chú dành cho Editor:** Dưới câu kịch bản bạn đang làm hình ảnh, bạn tạo **1 Toggle list** với tên quy định là **Trên màn hình (Editor)**.
        
        [2025-12-21 15-08-00.mp4](Gi%C3%A1o%20%C3%81n/2025-12-21_15-08-00.mp4)
        
    4. **Đánh số thứ tự (Cột mốc):** Bên trong Toggle list vừa tạo, bạn sử dụng các số trong ngoặc vuông [1], [2], [3]... để đánh dấu ngay trước vị trí sẽ xảy ra sự kiện. Các con số này đóng vai trò:
        - Đại diện cho tên Frame tương ứng trong file Figma.
        - Là những "mỏ neo" cố định thời điểm **bắt đầu** chuyển sang Frame kế tiếp.
- **Ví dụ thực tế:**
    - **Kịch bản:** Đừng để Code Bẩn trở thành DẤU CHẤM HẾT cho sự nghiệp lập trình của bạn!
    - **Kịch bản sau khi cắm mốc:** *[1] Đừng để Code Bẩn trở thành [2] DẤU CHẤM HẾT cho sự nghiệp lập trình của bạn!*
    - **Hình ảnh của Frame 1 và Frame 2 trong file Figma:**
        
        ![Screen Shot 2025-12-21 at 15.13.53.png](Gi%C3%A1o%20%C3%81n/Screen_Shot_2025-12-21_at_15.13.53.png)
        
    - **👉 Giải thích:**
        - Khi bắt đầu nói chữ “Đừng”: Editor sẽ biết “À, đoạn này sẽ hiển thị giống Frame [1]”
        - Tương tự, khi bắt đầu nói chữ “DẤU” → Hiển thị giống Frame [2].
        - Tuy nhiên, bạn cần lưu ý rằng không phải khi nói đến chữ “DẤU” là sẽ hiển thị video giống Frame [2] ngay lập tức. Đến mốc này, các thành phần BẮT ĐẦU chuyển động dần dần để tạo thành bố cục như Frame [2], và Editor sẽ tự làm các chuyển động này.
            
            [Ví dụ.mp4](Gi%C3%A1o%20%C3%81n/Vi_du.mp4)
            
- **Lợi ích:** Quy trình này loại bỏ hoàn toàn sự phỏng đoán. Designer và Editor sẽ biết chính xác từng mili giây cần có sự thay đổi gì trên màn hình.

### 2.2 Bước 2: Ánh xạ với thiết kế

Sau khi có các cột mốc, chúng ta sẽ xây dựng các hình ảnh Frame tương ứng với mỗi cột mốc.

- **Cách thực hiện:**
    1. **Tạo các Frame tương ứng:** Trong công cụ thiết kế (Figma), hãy tạo ra các Frame và đặt tên chúng trùng khớp với các số đã đánh dấu trong kịch bản.
    2. **Thiết kế hình ảnh cho từng mốc:** Lúc này, bạn hãy thiết kế hình ảnh chi tiết cho từng Frame.
- **Lợi ích:** Tạo ra một liên kết trực tiếp 1:1 giữa văn bản và thiết kế. Khi cần góp ý hay chỉnh sửa, mọi người có thể giao tiếp cực kỳ hiệu quả: "Check lại Frame số … nhé" thay vì mô tả dài dòng "Cái đoạn mà nói về cách đặt tên ấy...".

### 2.3 Bước 3: Chú thích thêm (Nếu cần thiết)

Về cơ bản, các Frame thiết kế là nội dung tĩnh. Editor sẽ chịu trách nhiệm làm cho chúng trở nên sinh động bằng cách thêm các hiệu ứng chuyển động phù hợp.

Tuy nhiên, đối với những phân cảnh đòi hỏi một số hiệu ứng đặc biệt để nhấn mạnh ý đồ kịch bản, bạn hoàn toàn có thể chỉ định rõ ràng. Hãy ghi chú trực tiếp vào kịch bản để đảm bảo những chuyển động quan trọng này được thực hiện chính xác theo mong muốn.

- **Cách thực hiện:**
    1. Bên trong Toggle list, bạn tạo các bullet.
    2. Mỗi bullet sẽ chứa các nội dung mà bạn muốn ghi chú lại cho Editor biết. Có thể đính kèm link tham khảo để rõ ràng hơn.
        
        👉 Tốt nhất đối với các trường hợp phức tạp, hãy chủ động nhắn tin với Editor để trao đổi trực tiếp. Tuy nhiên, vẫn phải ghi chú lại rõ ràng trong kịch bản để Editor không quên.
        
- **Ví dụ:**
    
    ![Screen Shot 2025-12-21 at 15.31.48.png](Gi%C3%A1o%20%C3%81n/Screen_Shot_2025-12-21_at_15.31.48.png)
    

**📌 Lưu ý:**

- Hãy tham khảo các dự án trước đó để rõ hơn:
    - **Video ngắn:**
        - **Video:**
            
            [https://www.youtube.com/shorts/6ZP3UxxPaHo](https://www.youtube.com/shorts/6ZP3UxxPaHo)
            
        - **Script: [Script Video Ngắn](T%C3%A0i%20Li%E1%BB%87u%20M%E1%BA%ABu/Script%20Video%20Ng%E1%BA%AFn%202d0b9e967cbc80f59e3de83dcf2d84b9.md)**
        - **Figma (Tải về và import vào Figma):** [Link](https://drive.google.com/file/d/1gQ5dTT3EeLqDmFH_tikmhU0s3tdB14lj/view?usp=sharing)
    - **Video dài:**
        - **Video:**
            
            [https://www.youtube.com/watch?v=ylJOHPioZ7s](https://www.youtube.com/watch?v=ylJOHPioZ7s)
            
        - **Script:** [Script Video Dài](T%C3%A0i%20Li%E1%BB%87u%20M%E1%BA%ABu/Script%20Video%20D%C3%A0i%202d0b9e967cbc803d9817c453db486367.md)
        - **Figma:** [Link](https://drive.google.com/file/d/1gQ5dTT3EeLqDmFH_tikmhU0s3tdB14lj/view?usp=sharing)

**📌 Lưu ý:**

- **👉 Làm bài tập: [Bài Tập](B%C3%A0i%20T%E1%BA%ADp%202d0b9e967cbc80bc9e0bc6908cf906be.md)**

---

# **Tối Ưu Trải Nghiệm Người Xem & Quy định đặt tên File**

## 1. Mục tiêu

- **Gia tăng tỷ lệ giữ chân (Retention):** Nắm vững quy tắc "Chống chán" để duy trì sự chú ý của khán giả xuyên suốt video, loại bỏ hoàn toàn các "màn hình chết".
- **Thắng ngay từ giây đầu tiên:** Hiểu và áp dụng thành thạo chiến thuật "Hook" (Mồi câu) cho từng định dạng video (Ngắn/Dài) để giảm tỉ lệ người xem bỏ qua.
- **Tối ưu quy trình phối hợp (Workflow):** Biết cách xử lý và định danh các file Video/GIF trong bản thiết kế tĩnh (Figma) để Editor nhận biết và thực hiện chính xác.

## 2. Nội dung

### **2.1 Nguyên Tắc "Chống Chán"**

- 📌 **Quy tắc:** **Đừng bao giờ để màn hình "chết" quá lâu.** Bộ não con người rất nhanh chán, và một màn hình **tĩnh** hoặc **không có sự thay đổi** chính là tín hiệu để họ lướt đi.
- **Cách thực hiện:** **Mỗi câu** trong kịch bản, hoặc tương ứng **mỗi 5-7 giây**, màn hình phải có từ **một cho đến hai sự thay đổi**, dù là nhỏ nhất:
    - Một icon mới bay vào.
    - Một dòng chữ được tô đậm hoặc thay đổi màu sắc.
    - Một cú zoom nhẹ vào chi tiết quan trọng.
    - Một hiệu ứng chuyển cảnh đơn giản.
    - …
- **Nói 1 cách cụ thể hơn:** Mỗi câu trong kịch bản cần phải có từ 1-2 Frame tương ứng trong file **Figma**.
- **📌 Mẹo tâm lý:** Hãy liên tục đặt mình vào vị trí của khán giả và tự hỏi: *"Nếu là họ, mình có bắt đầu thấy chán ở đoạn này không?"*. Cảm nhận của người xem chính là thước đo quan trọng nhất.

### **2.2 Chiến thuật mở đầu (Hook)**

3-5 giây đầu tiên quyết định 80% việc người xem có ở lại hay không. Vì vậy, phần mở đầu phải được tối ưu đến từng chi tiết để "câu" sự chú ý của họ ngay lập tức.

- **Dành cho video dài - "Từ Bìa vào Bài":**
    - **Chiến lược:** Các cảnh đầu tiên của video dài nên là phiên bản chuyển động của chính ảnh bìa (thumbnail). Khi người xem nhấp vào vì tò mò về thumbnail, hãy cho họ thấy chính xác điều đó ngay lập tức. Điều này tạo cảm giác quen thuộc và xác nhận rằng **"bạn đã đến đúng nơi"**.
    - **Ví dụ:**
        - **Thumbnail:**
            
            ![image.png](Gi%C3%A1o%20%C3%81n/image.png)
            
        - **2 Frame đầu tiên:**
            
            ![Screen Shot 2025-12-21 at 15.13.53.png](Gi%C3%A1o%20%C3%81n/Screen_Shot_2025-12-21_at_15.13.53.png)
            
        - **Kết quả cuối cùng:**
            
            [Ví dụ.mp4](Gi%C3%A1o%20%C3%81n/Vi_du.mp4)
            
- **Dành cho video ngắn:**
    - **Chiến lược:** Ngay từ giây đầu tiên, hãy đưa ra một hình ảnh khơi gợi sự tò mò hoặc một câu hỏi lớn. Có thể kết hợp hình ảnh này với dòng tiêu đề (Nên chứa keyword quen thuộc với nhóm khách hàng mục tiêu), khớp với những gì bạn đã hứa trong kịch bản.
    - **Ví dụ:**
        
        [https://www.youtube.com/shorts/6ZP3UxxPaHo](https://www.youtube.com/shorts/6ZP3UxxPaHo)
        
        [https://www.youtube.com/shorts/IjQsczxKu7Q](https://www.youtube.com/shorts/IjQsczxKu7Q)
        

### 2.3 Quy định đặt tên file Video/GIF

Khi thiết kế, đôi lúc bạn sẽ cần tải về các file **Video** hoặc ảnh **GIF**. Những file này bạn không thể đem trực tiếp vào bên trong Figma, tại vì Figma chỉ hỗ trợ ảnh tĩnh.

Vậy bạn cần làm như thế nào để Editor biết đối tượng đồ họa đó là Video hay ảnh GIF trong một Frame?

- **Cách thực hiện:**
    1. Bạn mở video, dùng chức năng chụp màn hình → chụp lại một cảnh bất kỳ trong video.
    2. Bạn đem ảnh đó vào Figma và xử lý như một đối tượng đồ họa bình thường.
    3. Bạn thêm hậu tố `_video` cho tên của đối tượng đồ họa đó → Editor sẽ biết đây là một video hoặc ảnh GIF.
        - **Ví dụ:** Tên file video là `letdiv` → tên đối tượng đồ họa tương ứng trong Figma là `letdiv_video`.
            
            ![Screen Shot 2025-12-21 at 16.19.09.png](Gi%C3%A1o%20%C3%81n/Screen_Shot_2025-12-21_at_16.19.09.png)
            
    4. Sau đó, bạn chuyển file Video/GIF vào thư mục quy định có tên **Assets** của dự án. Bạn lưu ý, thư mục Assets chỉ chứa các file có định dạng Video/GIF, không chứa ảnh tĩnh. Tại vì Editor có thể export ảnh tĩnh trực tiếp từ Figma.
- **📌 Lưu ý:** Bạn có thể tham khảo file Figma từ các dự án đã đề cập trước đó.

---

# Vùng An Toàn Cho Video Ngắn (Safe Zone)

## 1. Mục Tiêu

- **Hiểu rõ rủi ro:** Nhận thức được việc các thành phần giao diện (nút tim, comment, caption...) sẽ che mất nội dung nếu thiết kế không cẩn thận.
- **Thành thạo kỹ thuật:** Biết cách sử dụng lớp phủ (Overlay) Vùng an toàn trong Figma để kiểm tra thiết kế trước khi xuất file.

## 2. Nội dung

### 2.1. Khái niệm: Vùng An Toàn là gì?

Khi bạn xem video trên TikTok, Reels hay YouTube Shorts, màn hình không bao giờ hiển thị trọn vẹn 100% hình ảnh. Nó luôn bị che khuất bởi các thành phần giao diện (UI) mặc định của ứng dụng.

- **Vùng Chết (Dead Zone):** Là những khu vực bị che khuất.
    - **Cạnh Phải:** Các nút tương tác (Tim, Comment, Share, Save).
    - **Cạnh Dưới:** Tên kênh, Caption (mô tả video), thanh trượt thời gian.
    - **Cạnh Trên:** Tai thỏ, đồng hồ, pin, thanh tìm kiếm.
- **Vùng An Toàn (Safe Zone):** Là khu vực **trung tâm**, nơi bạn có thể đặt Text, Logo, Hình ảnh quan trọng mà đảm bảo 100% người xem sẽ nhìn thấy trọn vẹn trên mọi thiết bị.
- **📌 Lưu ý:**
    - Bạn có thể đặt các thành phần đồ họa vào **“Vùng Chết”** nhưng **hạn chế**.
    - Đối với các nội dung văn bản (Text), bạn không được đặt vào **“Vùng Chết”**, ****người xem sẽ không đọc được nội dung → Gây ức chế → Lướt qua. Công sức làm video coi như bỏ đi.

### 2.2. Hướng dẫn khoanh vùng an toàn trong Figma

Bạn không cần phải ngồi ước lượng bằng mắt. Hãy dùng tấm ảnh sau để thiết lập vùng An Toàn.

- **Bước 1:** Tải template [tại đây](https://drive.google.com/file/d/1eeQ7NemPG3sraOLVGvjnij8gbq8dJxzv/view?usp=sharing).
- **Bước 2:** Đưa ảnh vào Frame tương ứng trong Figma. Căn chỉnh sao cho khớp 4 góc với Frame.
- **Bước 3: Thiết lập Layer (Quan trọng)**
    - **Vị trí:** Đảm bảo Layer Safe Zone nằm ở **trên cùng** (Top) trong danh sách Layer.
    - **Khóa Layer:** Bấm vào biểu tượng ổ khóa 🔒 để tránh lỡ tay di chuyển nó.
    - **Chỉnh độ mờ (Opacity):** Chỉnh Opacity của Layer này xuống khoảng **50-70%**. Mục đích là để nó mờ đi, giúp bạn nhìn thấy thiết kế bên dưới.

**📌 Lưu ý:**

- Sau khi hoàn thành xong, vui lòng ẩn đi Layer Safe Zone.
- **👉 Làm bài tập: [Bài Tập](B%C3%A0i%20T%E1%BA%ADp%202d0b9e967cbc80bc9e0bc6908cf906be.md)**