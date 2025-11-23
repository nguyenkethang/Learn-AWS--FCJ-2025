---
title: "Nhật ký web 3"
date: 2025-07-02
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# Di chuyển trung tâm dữ liệu suôn sẻ: Thấu hiểu toàn bộ hành trình

**Tác giả:** Damien Renner và Matt Collins  
**Ngày đăng:** ngày 02 tháng 7 năm 2025  
**Danh mục:** AWS Transform, Best Practices, Customer Solutions, Enterprise Strategy, Experience-Based Acceleration, Migration, Migration & Transfer Services, Migration Portfolio Assessment, Self-serve Migration

## Giới thiệu

Di chuyển trung tâm dữ liệu là một công cuộc mang tính chuyển đổi, ảnh hưởng đến mọi khía cạnh của cơ sở hạ tầng CNTT, hoạt động và có khả năng là toàn bộ mô hình kinh doanh của một tổ chức. Khác với các nâng cấp công nghệ truyền thống, di chuyển lên đám mây là những thay đổi căn bản trong cách các tổ chức tiếp cận điện toán, lưu trữ, bảo mật và đổi mới công nghệ. Để tối đa hóa giá trị đám mây đồng thời giảm thiểu gián đoạn, cần có một phương pháp tiếp cận toàn diện, bao gồm việc trang bị năng lực cho các đội ngũ, triển khai quy trình kinh doanh, xác thực khả năng vận hành và hơn thế nữa. Việc tập trung vào toàn bộ hành trình và coi dự án là một sáng kiến chuyển đổi số quy mô lớn là rất quan trọng để đảm bảo việc áp dụng đám mây thành công, bền vững và chiến lược, mang lại giá trị kinh doanh hữu hình.

Trong bài blog này, chúng tôi sẽ phác thảo một hành trình di chuyển trung tâm dữ liệu điển hình dựa trên kinh nghiệm hỗ trợ hàng nghìn khách hàng doanh nghiệp, tận dụng khuôn khổ phương pháp di chuyển của AWS. Trong khi đọc bài đăng này, chúng tôi khuyên bạn nên đối chiếu dự án di chuyển của mình với từng thành phần. Điều này sẽ cho biết tình trạng tổng thể của dự án và giúp xác định các lĩnh vực cần tập trung.

## Hành trình di chuyển trung tâm dữ liệu lên đám mây điển hình

![Tổng quan hành trình di chuyển trung tâm dữ liệu](images/image3.png)

### Đào tạo & Trang bị năng lực

Đào tạo và trang bị năng lực cho đội ngũ CNTT và kinh doanh của bạn là một thành phần quan trọng của dự án di chuyển lên đám mây. Mặc dù AWS Transform loại bỏ nhu cầu đầu tư vô số giờ để nâng cao kỹ năng cho đội ngũ của bạn trở thành chuyên gia di chuyển vì nó đóng vai trò là cố vấn ảo đáng tin cậy của bạn, điều quan trọng là phải đảm bảo đội ngũ của bạn có đủ kiến thức và kinh nghiệm về AWS để vận hành hiệu quả các khối lượng công việc đã di chuyển và tối đa hóa giá trị đám mây. Chúng tôi khuyên bạn nên chủ động và có chủ đích trong việc đào tạo đội ngũ của mình vì đây là một bước quan trọng và có thể mất nhiều tháng để triển khai. AWS Learning Needs Analysis là một điểm khởi đầu tuyệt vời, nó sẽ khảo sát nhân viên của bạn về các kỹ năng đám mây của họ và xác định các lĩnh vực cần thiết với một kế hoạch học tập tùy chỉnh.

### Chuyển đổi Doanh nghiệp

Để tối đa hóa giá trị đám mây, bạn có thể cần phải chuyển đổi tổ chức và cách làm việc của mình. Ví dụ, điều chỉnh chiến lược đám mây với các ưu tiên chiến lược, đạt được sự đồng thuận giữa các bên liên quan về CNTT và Kinh doanh, cập nhật mô hình vận hành của bạn để phù hợp với các thực tiễn tốt nhất trên đám mây, xây dựng văn hóa số trong toàn bộ tổ chức và triển khai các best practice về Cloud FinOps. Điều quan trọng là phải có chủ đích và chủ động về những yếu tố này để tối đa hóa giá trị đám mây về lâu dài.

### Xác định Phạm vi & Chiến lược Di chuyển

Việc xác định phạm vi của dự án di chuyển là rất quan trọng để tạo điều kiện thuận lợi cho tất cả các giai đoạn tiếp theo. Mặc dù điều này khá đơn giản đối với một số khách hàng vì họ di chuyển mọi tài sản trong trung tâm dữ liệu của mình, nhưng những khách hàng khác thường sử dụng dự án di chuyển như một cơ hội để hợp lý hóa danh mục ứng dụng, điều này đòi hỏi một phân tích sâu hơn. Để hỗ trợ điều này, chúng tôi khuyên bạn nên tận dụng các chiến lược di chuyển 7R của chúng tôi.

### Đánh giá Mức độ Sẵn sàng của Tổ chức

Việc đánh giá mức độ sẵn sàng của tổ chức trong giai đoạn đầu của dự án di chuyển cho phép bạn tạo ra một kế hoạch có mục tiêu cho các thành phần thường chậm triển khai hơn. Chúng tôi khuyên bạn nên trao đổi với AWS Partner hoặc Account Manager của bạn về chương trình Migration Readiness Assessment (MRA) để xác định các điểm mạnh và điểm yếu từ góc độ sẵn sàng trên đám mây, và xây dựng một kế hoạch hành động để giải quyết bất kỳ khoảng trống nào được xác định.

### Khám phá Các khối lượng công việc trong Phạm vi

Khách hàng thường không có hiểu biết rõ ràng về mọi khối lượng công việc trong trung tâm dữ liệu của họ, cơ sở hạ tầng nền tảng cho từng khối lượng công việc (máy chủ, cơ sở dữ liệu, lưu trữ chung, bộ cân bằng tải, v.v.), các phụ thuộc mà một khối lượng công việc có trong toàn bộ hệ thống, và các yêu cầu về cấp phép. Trong kịch bản này, bạn có thể cần thực hiện một giai đoạn khám phá để đảm bảo đội ngũ di chuyển của bạn có dữ liệu cần thiết. Thực hiện đúng giai đoạn này có thể tăng tốc đáng kể tốc độ di chuyển của bạn ở các giai đoạn sau, và AWS Transform Assessments có thể đơn giản hóa bước này bằng cách phân tích môi trường CNTT của bạn để cung cấp các hiểu biết dựa trên dữ liệu và các khuyến nghị có thể hành động.

### Tạo Lập Luận Chứng Kinh doanh cho Việc Di chuyển

Giá trị của đám mây vượt ra ngoài việc giảm Tổng Chi phí Sở hữu (TCO). Khách hàng của AWS cũng nhận thấy những cải tiến đáng kể trong các lĩnh vực khác, bao gồm năng suất của nhân viên, khả năng phục hồi hoạt động và sự linh hoạt trong kinh doanh. Giai đoạn lập luận chứng kinh doanh cho việc di chuyển giúp điều chỉnh các bên liên quan trong toàn tổ chức và là một cơ hội tuyệt vời để đánh giá lại sự phù hợp của chiến lược di chuyển định hướng với các mục tiêu của tổ chức. Chúng tôi khuyên bạn nên đọc hướng dẫn Business Value on AWS và tận dụng AWS Transform để mô hình hóa tài chính chi tiết các khối lượng công việc của bạn nhằm tối đa hóa việc tiết kiệm chi phí.

### Triển khai Nền tảng AWS

Trước khi bạn có thể di chuyển khối lượng công việc lên đám mây, bạn sẽ cần triển khai nền tảng AWS của mình. Điều này bao gồm việc tạo ra một AWS Landing Zone được kiến trúc tốt, thiết lập kết nối mạng và xây dựng các dịch vụ chung mà ứng dụng của bạn yêu cầu. Giải pháp Landing Zone Accelerator on AWS triển khai một bộ khả năng nền tảng được thiết kế để phù hợp với các thực tiễn tốt nhất của AWS và nhiều khuôn khổ tuân thủ toàn cầu. Với Giải pháp AWS này, bạn có thể quản lý và quản trị tốt hơn môi trường nhiều tài khoản (multi-account) của mình vốn có các khối lượng công việc được quản lý chặt chẽ và các yêu cầu tuân thủ phức tạp.

### Triển khai Nền tảng Di chuyển

Việc triển khai nền tảng di chuyển mạnh mẽ như kế hoạch di chuyển, các mô hình di chuyển và tự động hóa di chuyển là rất quan trọng khi chuyển đổi trung tâm dữ liệu của bạn sang AWS và cho phép dự án của bạn mở rộng quy mô một cách hiệu quả và có cấu trúc. Các thành phần này phác thảo những khối lượng công việc nào sẽ được di chuyển, khi nào, và cách chúng sẽ được di chuyển. AWS Transform loại bỏ sự phỏng đoán khỏi các quyết định di chuyển lên đám mây bằng những hiểu biết sâu sắc có thể hành động giúp định hướng chiến lược di chuyển của bạn và giúp bạn tự tin lập kế hoạch di chuyển dựa trên các khối lượng công việc trong phạm vi của bạn.

### Thực thi Di chuyển & Hiện đại hóa

Đây là giai đoạn mà tất cả các khía cạnh trước đó được đưa vào thử nghiệm, tận dụng các mô hình và tự động hóa đã được tạo ra ở bước trước. Đừng ngần ngại xem xét lại các thành phần trước đó nếu phát hiện ra thách thức (ví dụ: các hoạt động khám phá bổ sung nếu bạn không có đủ dữ liệu để di chuyển các khối lượng công việc thử nghiệm hoặc đánh giá lại phương pháp đào tạo nếu xác định được khoảng cách kỹ năng). Chúng tôi khuyên bạn nên bắt đầu với AWS Experience-Based Accelerator (EBA) để tạo đà và sử dụng AWS Transform để tận dụng các tác nhân AI nhằm tự động hóa các tác vụ phức tạp (như tạo cơ sở hạ tầng dưới dạng mã, phân tích mã ứng dụng, phân tách, tái cấu trúc, xác thực và triển khai).

### Kiểm thử Chức năng & Phi chức năng

Mặc dù kiểm thử chức năng và phi chức năng của một khối lượng công việc thường được yêu cầu trước các đợt chuyển đổi chính thức (production cutover) khối lượng máy chủ đang được di chuyển có thể đặt ra những thách thức ở cấp độ dự án. Hãy xem xét việc tạo ra một chiến lược kiểm thử toàn diện càng sớm càng tốt, phác thảo các ưu tiên, các kịch bản cần kiểm thử và nơi áp dụng. Ví dụ, áp dụng ưu tiên cao hơn cho các khối lượng công việc quan trọng đối với kinh doanh và một phương pháp 'fix-forward' (sửa lỗi ở phiên bản sau) cho các tải công việc không trọng yếu để cân bằng giữa tính liên tục của kinh doanh và tốc độ di chuyển.

### Xác thực Các Yêu cầu về Bảo mật & Tuân thủ

Bảo mật và tuân thủ không phải là những ô kiểm tra mà là những mệnh lệnh chiến lược cho tất cả các doanh nghiệp. Việc xác thực các yêu cầu bảo mật được đáp ứng là một thành phần quan trọng trong tất cả các hành trình áp dụng đám mây. Nếu bạn chưa làm, chúng tôi khuyên bạn nên xem AWS Security Hub để tập trung hóa các kiểm tra và cảnh báo bảo mật của bạn, và đánh giá chương trình quản trị nội bộ của bạn khi nó chuyển đổi từ môi trường tại chỗ (on-premises) lên đám mây với AWS Shared Responsibility Model. Nếu bạn có các yêu cầu tuân thủ như PCI DSS hoặc HIPAA, AWS Security Assurance Services (AWS SAS) cung cấp quyền truy cập vào các kiểm toán viên giàu kinh nghiệm kết hợp với chiều sâu kỹ thuật của AWS để hỗ trợ các yêu cầu tuân thủ của bạn.

### Xác thực Khả năng Phục hồi Ứng dụng & Mức độ Sẵn sàng Vận hành

Trung tâm dữ liệu của bạn có thể chứa các tải công việc trọng yếu (mission-critical workloads) phải được thiết kế với độ sẵn sàng cao (high-availability). Khi di chuyển các khối lượng công việc này, chúng tôi khuyên bạn nên thực hiện các bài đánh giá theo Well-Architected Framework để xác thực việc triển khai khối lượng công việc, và các đánh giá khả năng phục hồi ứng dụng để xác thực các khía cạnh công nghệ, con người và quy trình có phù hợp với mục tiêu phục hồi của bạn hay không. Điều này có thể bao gồm việc thực hiện các buổi game day mô phỏng (simulated game-days) nơi kịch bản từ đầu đến cuối được kiểm tra (giám sát, cảnh báo, phản hồi, khắc phục, v.v.).

### Vận hành Các Khối lượng Công việc đã Di chuyển

Mỗi khối lượng công việc đã di chuyển cần được vận hành bởi một đội ngũ có kiến thức và kinh nghiệm về AWS để đảm bảo hoạt động suôn sẻ. Chúng tôi khuyên bạn nên lập kế hoạch trước cho giai đoạn này và tạo ra một kế hoạch di chuyển cho phép đội ngũ của bạn dần dần xây dựng kinh nghiệm, chẳng hạn như bắt đầu với các khối lượng công việc có độ ưu tiên thấp và độ phức tạp thấp. Ngoài ra, AWS Managed Services (AMS) có thể cung cấp hỗ trợ vận hành tạm thời để cho phép đẩy nhanh tiến độ di chuyển và giải phóng đội ngũ của bạn khỏi các hoạt động đám mây hàng ngày, như giám sát, quản lý sự cố và vấn đề, vá lỗi, sao lưu và quản lý bảo mật.

### Ngừng hoạt động Cơ sở hạ tầng Gốc

Nhiều lập luận chứng kinh doanh phụ thuộc vào việc ngừng hoạt động cơ sở hạ tầng gốc, nhưng bạn sẽ ngạc nhiên khi biết có bao nhiêu khách hàng không chủ động lập kế hoạch cho giai đoạn này của dự án. Chúng tôi khuyên bạn nên đảm bảo kế hoạch di chuyển của mình phù hợp với các yêu cầu giải thể/thanh lý trung tâm dữ liệu và triển khai một quá trình chuyển giao hiệu quả từ đội ngũ di chuyển sang đội ngũ ngừng hoạt động để đơn giản hóa giai đoạn này.

## Kết luận

Bài blog này đã cung cấp một cái nhìn tổng quan về hành trình điển hình của khách hàng khi di chuyển trung tâm dữ liệu lên đám mây. Bằng cách hiểu rõ từng thành phần của hành trình di chuyển, bạn có thể giảm thiểu gián đoạn tốt hơn và tối đa hóa giá trị chiến lược của quá trình chuyển đổi đám mây của mình.

Chúng tôi khuyên bạn nên đánh giá dự án di chuyển trung tâm dữ liệu của mình dựa trên các thành phần được phác thảo trong bài blog và chia sẻ những phát hiện này với AWS Account Manager của bạn để nhận các đề xuất dựa trên kinh nghiệm của chúng tôi trong việc di chuyển hàng nghìn khách hàng doanh nghiệp lên đám mây.

---

### Về tác giả

**Damien Renner**

![Damien Renner](images/image1.png)

Với vai trò Giám đốc Sản phẩm Kỹ thuật Cấp cao tại AWS, Damien Renner hỗ trợ các doanh nghiệp lớn điều hướng các sáng kiến chuyển đổi số phức tạp và áp dụng đám mây. Ông là một chuyên gia về di chuyển trung tâm dữ liệu và hỗ trợ khách hàng thuộc nhiều ngành công nghiệp khác nhau. Trong thời gian rảnh rỗi, Damien thường leo núi hoặc lên kế hoạch cho chuyến phiêu lưu du lịch tiếp theo của mình.

**Matt Collins**

![Matt Collins](images/image2.png)

Với vai trò Trưởng bộ phận Dịch vụ Toàn cầu của AWS (Leader of AWS Global Services Offerings), Matt Collins giúp các tổ chức trên toàn thế giới chuyển đổi doanh nghiệp của họ thông qua AI và công nghệ đám mây. Là một nhà công nghệ đầy đam mê với hơn 35 năm kinh nghiệm trong Phát triển Phần mềm, chiến lược CNTT và Đổi mới, ông đã hướng dẫn một số doanh nghiệp lớn nhất thế giới qua quá trình tiến hóa số của họ. Khi không bận định hình tương lai của AI và các dịch vụ đám mây, Matt thường dành thời gian cố vấn cho các tài năng công nghệ trẻ và khám phá các công nghệ đột phá.

---
