### Vấn đề 80% trong kỷ nguyên lập trình bằng AI: Nhanh hơn, nhưng có thật sự dễ hơn?

Gần đây, khi nhìn lại cách mình làm việc, mình thấy một thay đổi rất rõ: trước đây mình tự code là chính, còn AI chỉ hỗ trợ. Bây giờ thì ngược lại, AI xử lý phần lớn bản nháp, mình tập trung chỉnh sửa và kiểm soát chất lượng.

Mình tin nhiều bạn dev cũng đang ở trạng thái giống vậy: mỗi ngày mở ra một loạt PR mới, nhiều đoạn code do AI tạo ra gần như hoàn toàn.

Chúng ta đã đi qua mốc "AI chỉ làm được 70%". Ở nhiều dự án mới, AI đã chạm mốc 80%, thậm chí 90% ở một số tác vụ.

Nhưng năng suất tăng không đồng nghĩa mọi thứ dễ hơn. Vấn đề không mất đi, nó chỉ đổi dạng.

#### Lỗi không còn nằm ở cú pháp, mà nằm ở cách nghĩ

Trước kia, AI hay sai cú pháp. Bây giờ, AI thường gặp những lỗi "có vẻ hợp lý" nhưng dễ gây hậu quả về sau.

**1) Sai giả định ngay từ đầu**

Bạn yêu cầu làm tính năng đăng nhập. AI mặc định hệ thống dùng email + mật khẩu, rồi triển khai trọn gói theo hướng đó: database, API, giao diện.

Vài ngày sau, khi đã merge vài PR, bạn mới nhớ ra: hệ thống cần đăng nhập bằng số điện thoại.

Lúc này, sai không nằm ở một dòng code. Sai nằm ở hướng thiết kế từ ban đầu.

**2) Làm quá mức cần thiết**

Có lúc bạn chỉ cần một hàm nhỏ. AI lại sinh ra cả một bộ class, interface, tầng xử lý nhiều lớp. Nhìn "pro" nhưng khó bảo trì.

Mẹo đơn giản: bạn cứ hỏi thẳng "Có cách nào đơn giản hơn không?". Thường thì AI sẽ viết lại gọn hơn ngay.

**3) Đồng ý quá nhanh, ít phản biện**

Nếu prompt của bạn thiếu thông tin hoặc mâu thuẫn, AI vẫn có xu hướng lao vào làm ngay. Ít hỏi ngược, ít bắt lỗi yêu cầu.

Vì vậy, nếu bạn prompt sai, AI sẽ làm rất nhanh... theo hướng sai.

#### Món nợ hiểu biết: chi phí ẩn dễ bị bỏ qua

Viết code và đọc hiểu code là hai kỹ năng khác nhau.

Khi phụ thuộc AI quá nhiều, bạn vẫn có thể "review" code. Nhưng đến một ngưỡng, review biến thành "đọc lướt cho xong".

Đó là món nợ hiểu biết (comprehension debt).

Nó nguy hiểm vì đến rất im. Code trông hợp lý, test xanh, deadline gấp. Bạn merge.

Đến lúc có lỗi production, ai đó hỏi: "Đoạn này chạy thế nào?"

Nếu không giải thích được, nghĩa là bạn đang sở hữu một codebase mà chính mình không nắm chắc.

#### Nghịch lý năng suất: PR nhiều hơn, review mệt hơn

Một số dữ liệu cho thấy:

- Số lượng PR tăng mạnh khi team dùng AI.
- Thời gian review cũng tăng rất cao.
- Kích thước mỗi PR lớn hơn đáng kể.

Hình dung đơn giản: xe chạy nhanh hơn, nhưng đường đông hơn.

Nút thắt không còn ở chỗ viết code. Nút thắt nằm ở chỗ đọc, hiểu, xác minh và bảo trì code.

#### Hai cách dùng AI mà bạn sẽ thấy rất rõ

**Cách 1: Làm việc theo kiểu "mô tả kết quả"**

Thay vì bắt AI làm từng bước nhỏ, bạn đưa yêu cầu, tiêu chí thành công, test cần vượt qua, rồi để AI tự đề xuất cách làm.

**Cách 2: Dùng AI như autocomplete nâng cấp**

Vẫn prompt theo kiểu chỉ đạo từng dòng, từng hàm. Cách này vẫn hiệu quả, nhưng dễ bị giới hạn khi bài toán lớn dần.

Thực tế cho thấy: vai trò kỹ sư đang giống người quản lý kỹ thuật hơn. Giao bài toán, kiểm kết quả, và chỉnh hướng khi lệch.

#### Cách dùng AI để tăng tốc mà không mất kiểm soát

**1) Để AI viết bản nháp đầu tiên**

Thay vì xin từng đoạn nhỏ, bạn để AI tạo bản nháp trọn tính năng. Sau đó bạn tinh chỉnh.

**2) Prompt bằng mục tiêu, không prompt bằng cách làm**

Nói rõ "cần đạt gì" quan trọng hơn "phải code như nào".

**3) Gặp đoạn nào không hiểu thì dừng lại**

Đừng merge vội. Bạn yêu cầu AI giải thích, hoặc tự viết lại đoạn đó theo cách bạn hiểu.

**4) Giữ kiến trúc gọn và rõ**

Module rõ ràng, API rõ ràng, rule rõ ràng. Càng rõ, AI càng ít đi sai hướng.

**5) Luyện "cơ bắp" code thủ công định kỳ**

Thỉnh thoảng tự viết một tính năng từ đầu, hoặc tự viết test trước (TDD) rồi mới cho AI triển khai.

#### Kết

AI không thay thế kỹ sư. AI khuếch đại tốc độ của kỹ sư.

Nếu bạn có tư duy rõ, AI giúp bạn đi rất nhanh.
Nếu bạn mơ hồ, AI cũng sẽ đưa bạn đi nhanh... nhưng sai hướng.

Nguyên tắc đơn giản để nhớ:

**Dùng AI để tăng tốc, nhưng phải tự mình sở hữu kết quả.**

Trong giai đoạn này, người có lợi thế không phải người viết nhiều code nhất, mà là người hiểu bài toán rõ nhất và giữ được chất lượng khi tốc độ tăng cao.