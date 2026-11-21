# WHO'S LYING? — Bóng Tối Trong Đêm (v1.0)

Game trinh thám suy luận xã hội 4–8 người chơi qua trình duyệt. **Ảnh nền biệt thự** là ảnh gốc do người dùng cung cấp, nằm ở `public/assets/mansion.png`.

## Cài đặt

Cần Node.js 18+.

```bash
npm install
npm start
```

Mở **http://localhost:3000**. Người khác trong cùng Wi-Fi có thể mở `http://IP-LAN-CUA-MAY-CHU:3000` nếu tường lửa cho phép. Muốn chơi từ xa qua Internet cần triển khai server có HTTPS/WebSocket hoặc dùng đường hầm mạng đáng tin cậy.

## Cách chơi

1. Người đầu tiên tạo phòng, chia sẻ mã 6 ký tự. Mỗi người dùng tab hoặc thiết bị riêng.
2. 4–8 người cùng nhấn **Sẵn sàng**; chủ phòng bắt đầu. Vai trò và bí mật gửi riêng cho từng người.
3. **Thẩm vấn:** Điều Tra Viên chủ động nhắn riêng; Kẻ Hai Mang thăm dò riêng. Các người chơi khác trò chuyện chung, người nhận có thể trả lời. Kẻ Hai Mang gửi đề nghị thông tin dưới bí danh **Bóng Xám**. Giao dịch có thể chứa tin sai, không bị phạt vì sai.
4. **Khám phá:** Mở các khu vực, nhấp điểm tương tác để phát hiện chứng cứ chung. Vật chứng không tự chứng minh danh tính hung thủ.
5. **Đối chất:** Điều Tra Viên chọn người bị cáo buộc. Phòng 4–5 cần Hung Thủ 1; phòng 6 cần cả Hung Thủ 1 và 2; phòng 7–8 cần Ông Trùm. Phán quyết cần >=2 chứng cứ và đa số Điều Tra Viên chọn đúng toàn bộ mục tiêu, không thêm người khác.
6. Mọi người nhấn **Hoàn thành** để qua giai đoạn, không giới hạn thời gian.
7. Kẻ Hai Mang thắng độc lập nếu không bị vạch mặt **và** có ít nhất một giao dịch được chấp nhận bởi phe giành chiến thắng (Điều Tra Viên khi phe điều tra thắng, hoặc Hung Thủ/Ông Trùm khi phe phản diện thắng). Đây là cách lượng hóa sự hỗ trợ cho bản chơi điện tử, có thể điều chỉnh trong phiên bản sau.
8. **Vạch mặt:** mỗi người có một lần cáo buộc riêng; đúng vai Kẻ Hai Mang thì người bị vạch mặt mất điều kiện thắng. Kết quả chỉ thông báo cho người cáo buộc và Kẻ Hai Mang. Không có vật chứng tự động lộ danh tính.

## Vai trò

| Số người | Điều tra viên | Hung thủ 1 | Hung thủ 2 | Nhân chứng 1 | Nhân chứng 2 | Kẻ Hai Mang | Ông Trùm |
|---|---:|---:|---:|---:|---:|---:|---:|
| 4 | 1 | 1 | 0 | 1 | 0 | 1 | 0 |
| 5 | 2 | 1 | 0 | 1 | 0 | 1 | 0 |
| 6 | 2 | 1 | 1 | 1 | 0 | 1 | 0 |
| 7 | 2 | 1 | 1 | 1 | 0 | 1 | 1 |
| 8 | 2 | 1 | 1 | 1 | 1 | 1 | 1 |

## Giới hạn của v1.0

- Game **chơi được một vòng từ đầu đến cuối** nhưng là **bản đầu hoàn chỉnh vòng chơi**, chưa phải sản phẩm thương mại: không có đăng nhập, cơ sở dữ liệu, lưu ván, ghép phòng công khai, hoạt họa nhân vật, giọng nói hay AI giám sát lời khai.
- Trò chơi vận hành theo nguyên tắc suy luận xã hội: chứng cứ là dữ kiện gợi mở; hệ thống không thể tự xác định sự đúng/sai của lời nói tự do. Quy tắc phán quyết dựa trên danh tính đúng và số chứng cứ đã tìm được.
- Mỗi lượt vạch mặt được hệ thống xác nhận theo vai trò thực tế (không phân tích lý do bằng ngôn ngữ tự nhiên). Do đó người chơi nên tuân thủ tinh thần suy luận thay vì đoán mò.
- Dữ liệu nằm trong RAM; **server khởi động lại sẽ mất phòng**. Người chơi rời giữa ván sẽ đưa phòng về chờ để tránh ván bị kẹt. Hiện chưa hỗ trợ kết nối lại sau khi mất mạng.
- Chưa có cơ chế riêng để ngăn người được thẩm vấn nhận tin nhắn thăm dò cùng lúc; người chơi nên tự điều phối theo luật bàn chơi.
- Phòng 4–6 người không có Ông Trùm là người chơi, nên kết cục lật đổ tổ chức được quy ước theo việc Điều Tra Viên bắt đúng hung thủ hiện diện. Đây là cách quy đổi gameplay, không thay đổi canon cốt truyện.

## Cấu trúc

- `server.js`: Express, Socket.IO, phòng chơi, vai trò, giai đoạn, tin nhắn, giao dịch, vạch mặt, phán quyết.
- `public/index.html`: giao diện.
- `public/style.css`: phong cách noir, responsive.
- `public/app.js`: trạng thái và tương tác giao diện.
- `public/assets/mansion.png`: hình biệt thự gốc.
