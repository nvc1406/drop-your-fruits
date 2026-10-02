# Hoa quả · Thả nhẹ, ghép vui

MVP JavaScript thuần, Canvas 2D, Matter.js 0.20.0 và Vite. Không backend, không API, không tải ảnh/font ngoài. Điểm cao nhất được lưu bằng `localStorage` theo trình duyệt và địa chỉ web; không lưu ván chơi.

## Chạy source

Yêu cầu Node.js 22.12+ hoặc 20.19+.

```sh
npm install
npm run dev
```

Mở địa chỉ Vite hiển thị. Có thể thêm `-- --host 0.0.0.0` để thử bằng điện thoại trên cùng Wi-Fi nếu firewall cho phép.

## Build và đưa lên web

```sh
npm run build
npm run preview
```

Upload **nội dung thư mục `dist/`** lên hosting tĩnh. Đã cấu hình đường dẫn tương đối để chạy cả trong thư mục con. Bản production chứa thư viện vật lý, không phụ thuộc CDN.

Không mở trực tiếp `index.html` bằng `file://`; hãy dùng HTTP hosting/server. Node.js chỉ dùng cho phát triển và build, không cần trên hosting production.

## Luật đã chọn

- 10 cấp: Việt quất, Cherry, Chanh, Mận, Cam, Táo, Lê, Đào, Dừa, Dưa hấu. Hoa quả được minh hoạ bằng Canvas, có màu vỏ, cuống, lá và chi tiết riêng; không cần tải ảnh ngoài.
- Hai item cùng cấp chạm nhau thành một item lớn hơn; cấp 10 giữ nguyên.
- Chỉ cộng điểm khi ghép, theo item mới: 1, 3, 6, 10, 15, 21, 28, 36, 45, 55. Cấp 1 không được tạo bởi ghép nên không cộng 1 điểm khi thả.
- Item mới random trong 4 cấp đầu theo tỷ lệ 40%, 30%, 20%, 10%.
- Mép trên của một item vượt vạch liên tục 2 giây thì thua. Item mới được miễn kiểm tra cho đến khi vào dưới vạch, hoặc chạm vật khác sau 550ms, hoặc đã rơi 1200ms. Thời gian vượt vạch được giữ khi ghép nếu kết quả vẫn vượt vạch.
- Các lần thả cách nhau ít nhất 650ms để tránh bấm liên tục làm vật lý khó kiểm soát.
- Chuột: di chuyển, click để thả. Cảm ứng: kéo chọn chỗ, nhả để thả. Bàn phím: ← → và Space/Enter khi khung chơi được focus.
- Tạm dừng khi tab ẩn, và yêu cầu bấm chơi tiếp khi quay lại. Hướng dẫn cũng tạm dừng ván.

## Điều chỉnh

- `src/config.js`: cấp, kích thước, hình dạng, điểm, random, vạch thua và các thời gian.
- `src/world.js`: mô phỏng vật lý, hàng đợi ghép, điểm và thua.
- `src/draw.js`: hình vẽ hoa quả, cuống/lá, vân vỏ và hiệu ứng.
- `src/fruits.js`: nét minh hoạ riêng cho từng loại quả. Các hình được vẽ một lần vào canvas phụ rồi dùng lại khi rơi/xoay để giảm tải.
- `src/main.js`: input, giao diện, vòng lặp và lưu kỷ lục.
- `src/style.css`: layout máy tính/điện thoại.

Item là vật thể cứng gần tròn với các đường bao lồi khác nhau, không phải vật thể mềm biến dạng. Cuống và lá là trang trí; collider theo đường bao thân quả. Việc đổi hình hoa quả giữ nguyên kích thước và collider của phiên bản trước.

Mọi thư viện đều được đóng gói; Matter.js dùng MIT, xem `node_modules/matter-js/LICENSE` trong source hoặc `THIRD-PARTY-NOTICES.txt` trong bản phát hành.

## Kiểm tra

```sh
npm test
```

13 kiểm tra vật lý và luật: random 40/30/20/10, cooldown, ghép khi chạm, khác cấp, ba item chạm cùng lúc, ghép dây chuyền, cấp cuối, mép trên vượt vạch 2 giây, miễn kiểm tra lúc thả, reset cảnh báo, giữ thời gian cảnh báo qua lần ghép, ghép sát đáy và mô phỏng một ván dài đến khi thua.

Đã kiểm tra giao diện bằng trình duyệt ở kích thước desktop và viewport 390×844: bàn phím, con trỏ, tạm dừng, chơi tiếp và hướng dẫn. Chưa kiểm tra cảm ứng trên thiết bị điện thoại thật; cần thử thêm trước khi phát hành rộng.
