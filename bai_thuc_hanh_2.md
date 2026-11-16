Context:
Bạn là một chuyên gia phân tích dữ liệu thị trường của nền tảng Thương mại điện tử, chịu trách nhiệm phân tích phản hồi khách hàng để chuyển đến đúng phòng ban xử lý (Kỹ thuật, Chăm sóc khách hàng, Giao hàng, Kho vận) và cung cấp dữ liệu cho Dashboard thống kê.

Output:
Một JSON object thô (raw JSON) có đúng 4 key: sentiment, topics, score, summary.
Không dùng markdown, không bọc trong khối code, không dùng bất kỳ định dạng trang trí nào ngoài JSON thô.
Chỉ trả về dữ liệu kết quả, nghiêm cấm AI viết thêm các đoạn văn giải thích ở đầu hoặc cuối câu trả lời.
Không được tự ý thêm thắt hoặc suy đoán thông tin không có trong phản hồi của khách hàng.
Nếu phản hồi trống hoặc chứa ký tự đặc biệt không đọc được, trả về tag "Invalid" cho mọi trường.

Request:
Phân tích phản hồi của khách hàng và trích xuất các thuộc tính: Cảm xúc chính (sentiment), Chủ đề chính (topics), Điểm số hài lòng (score), Tóm tắt (summary).

Explanation:
Dữ liệu này được đưa trực tiếp vào Dashboard để vẽ biểu đồ mức độ hài lòng theo từng chủ đề nên cần độ chính xác 100%.
- sentiment chỉ được là: "Positive", "Negative" hoặc "Neutral".
- topics là mảng, chỉ được chọn từ: "Product", "Delivery", "Service", "System".
- Nếu phản hồi khen ngợi tốc độ giao hàng nhưng chê sản phẩm thì phải gắn cả hai tag tương ứng trong topics (ví dụ ["Product", "Delivery"]).
- score là số nguyên từ 1 đến 5 (1: rất không hài lòng, 5: rất hài lòng).
- summary tóm tắt ngắn gọn dưới 15 từ, lọc bỏ các từ cảm thán thừa thãi.

Tone:
Chính xác, khách quan, không thêm thắt văn phong cảm xúc.

Extras:
Ví dụ 1 (Positive):
Phản hồi: "Giao hàng siêu nhanh, tai nghe âm thanh tuyệt vời, rất đáng tiền!!!"
Kết quả: { "sentiment": "Positive", "topics": ["Delivery", "Product"], "score": 5, "summary": "Giao hàng nhanh, tai nghe âm thanh tốt, đáng tiền" }

Ví dụ 2 (Negative):
Phản hồi: "Giao hàng nhanh nhưng sản phẩm bị móp méo, thất vọng quá!"
Kết quả: { "sentiment": "Negative", "topics": ["Product", "Delivery"], "score": 2, "summary": "Giao hàng nhanh nhưng sản phẩm bị móp méo" }

Ví dụ 3 (Neutral):
Phản hồi: "Chuột dùng tạm được, không có gì đặc biệt."
Kết quả: { "sentiment": "Neutral", "topics": ["Product"], "score": 3, "summary": "Chuột dùng tạm được, không đặc biệt" }

Ví dụ 4 (Phản hồi trống hoặc không đọc được):
Phản hồi: "@@## ~~~"
Kết quả: { "sentiment": "Invalid", "topics": ["Invalid"], "score": "Invalid", "summary": "Invalid" }

Hãy phân tích phản hồi của khách hàng trong thẻ <feedback>...</feedback> dưới đây:

<feedback>
Giao hàng rất nhanh nhưng laptop bị móp góc, nhân viên hỗ trợ trả lời chậm quá!!!
</feedback>