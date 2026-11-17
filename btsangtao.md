BƯỚC 1: 2 MẪU PROMPT
- Giải pháp 1:
"Đọc email suy luận từng bước để tìm mã đơn, lỗi sản phẩm, đối chiếu chính sách bảo hành 12 tháng (không bảo hành rơi vỡ/vào nước) rồi viết email phản hồi khách."
- Giải pháp 2:
"Xử lý email theo 3 bước tuần tự:
- B1: Tìm [Mã đơn] và [Lỗi]. Thiếu 1 trong 2 -> xuất STATUS=ERROR và DỪNG xét duyệt. Đủ -> STATUS=OK.
- B2: Chỉ chạy khi STATUS=OK. Đối chiếu [Lỗi] với chính sách để chốt DUYỆT hoặc TỪ CHỐI.
- B3: Nếu ERROR, chỉ viết email hỏi thông tin thiếu (cấm tự suy đoán). Nếu OK, viết email báo kết quả B2."
BƯỚC 2: BẢNG SO SÁNH TRADE-OFF
| Tiêu chí | Giải pháp 1 (Đơn giản) | Giải pháp 2 (Chi tiết) | Đánh giá Trade-off |
| --- | --- | --- | --- |
| Độ dễ hiểu | Cao (Ngắn, viết nhanh). | Trung bình (Cần cấu trúc luồng rẽ nhánh). | Đổi sự đơn giản lúc viết lấy khả năng kiểm soát AI. |
| Tốn token | Ít (~40 tokens). | Nhiều hơn (~110 tokens). | Tốn chi phí hơn nhưng tránh thiệt hại do sai nghiệp vụ. |
| Chặn lỗi biên | Trung bình (Dễ bịa thông tin khi thiếu dữ liệu). | Cực tốt (Ngắt chuỗi an toàn bằng cờ ERROR). | Chặn đứng hiệu ứng "đứt gãy chuỗi" khi gặp input rác/thiếu. |
BƯỚC 3: LỰA CHỌN VÀ CHẠY THỬ
Lựa chọn: Giải pháp 2.
Lý do: Đảm bảo tính toàn vẹn của chuỗi (Prompt Chaining). Cờ STATUS=ERROR giúp ngắt mạch suy luận kịp thời khi dữ liệu đầu vào bị thiếu, triệt tiêu tình trạng AI tự suy diễn sai chính sách.
Kết quả chạy thử (Input bẫy thiếu mã đơn):
- Input: "Tai nghe tôi mới mua tự nhiên không lên nguồn, đổi cái mới cho tôi nhé!"
- Output AI:
  - B1: Thiếu [Mã đơn], Lỗi: không lên nguồn -> STATUS=ERROR
  - B2: (Ngắt - Không chạy).
  - B3: "Chào bạn, rất tiếc về sự cố tai nghe. Bạn vui lòng cung cấp Mã đơn hàng để shop kiểm tra bảo hành và hỗ trợ bạn ngay nhé!"
