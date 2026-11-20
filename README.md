# Jarvis

Jarvis là trợ lý cá nhân chạy hoàn toàn trên máy bạn: không tài khoản, không server, không cloud. Phần
AI chạy qua Claude Code bằng gói Claude của chính bạn, nên không tốn phí API.

**[Tải bản mới nhất](https://github.com/devTah/jarvis-releases/releases/latest)**: file
`Jarvis_<phiên bản>_x64-setup.exe`.

## Cần chuẩn bị gì

| Thứ cần có | Bắt buộc? | Ghi chú |
| --- | --- | --- |
| Máy Windows 10/11 (64-bit) | Có | Chưa có bản macOS |
| Gói Claude trả phí (Pro hoặc Max) | Có | Chat và agent dùng quota của gói này |
| Claude Code (lệnh `claude`) | Có | Thiếu nó thì Chat, agent, coding loop không chạy |
| Tailscale + iPhone | Không | Chỉ khi muốn dùng Jarvis trên điện thoại |
| Tài khoản Binance hoặc OKX | Không | Chỉ khi muốn mua thật; chế độ paper không cần |

Mỗi người dùng một bản riêng: dữ liệu, tailnet và key sàn của bạn không liên quan gì tới máy người khác.

## Bước 1: Cài Claude Code

Cài Claude Code trước, vì Jarvis gọi lệnh `claude` để làm mọi việc cần AI.

1. Mở PowerShell và cài theo hướng dẫn chính thức tại
   [docs.claude.com/claude-code](https://docs.claude.com/en/docs/claude-code/setup).
2. Gõ `claude` một lần và đăng nhập bằng tài khoản Claude (Pro hoặc Max).
3. Mở cửa sổ PowerShell mới, gõ `claude --version`. Ra số phiên bản là được.

Lệnh `claude` phải nằm trong PATH. Nếu Jarvis báo "The Claude Code CLI (claude) was not found on PATH",
quay lại bước 3.

## Bước 2: Tải và cài Jarvis

1. Vào [trang Releases](https://github.com/devTah/jarvis-releases/releases/latest) và tải file
   `Jarvis_<phiên bản>_x64-setup.exe`.
2. Chạy file vừa tải. Windows SmartScreen sẽ báo "Windows protected your PC" vì bộ cài chưa ký chứng
   chỉ Microsoft: bấm **More info** rồi **Run anyway**.
3. Làm theo trình cài. Nếu máy thiếu WebView2, trình cài tự tải về.
4. Mở Jarvis. Lần đầu app hỏi "Mở Jarvis cùng máy?": chọn có nếu muốn lịch hẹn, tin tức và thị trường
   chạy nền.

Đóng cửa sổ chỉ thu Jarvis xuống khay hệ thống, app vẫn chạy. Muốn thoát hẳn thì dùng menu của icon
dưới khay.

## Bước 3: Thiết lập lần đầu

Vào **Settings** và làm ba việc dưới đây. Xong là dùng được Chat ngay.

1. **Claude Code**: kiểm tra app thấy lệnh `claude` và báo đã đăng nhập. Nếu báo chưa cài, xem Bước 1.
2. **Folders**: thêm những thư mục bạn cho Jarvis đọc và sửa. Jarvis không đụng tới file ngoài các thư
   mục này.
3. **Permissions**: xem lại những việc cần bạn duyệt. Mặc định, mọi việc rủi ro (sửa file, chạy lệnh)
   đều chờ bạn bấm duyệt trên Home.

Muốn dùng coding loop hoặc QA, tạo một mục trong **Projects** và trỏ tới thư mục code (thư mục đó phải
nằm trong Folders). Mọi lần Claude Code chạy đều tính vào quota gói Claude của bạn; xem mức dùng ở
trang **Usage**.

## Tuỳ chọn: Dùng trên iPhone

iPhone mở Jarvis dưới dạng web app (PWA) do chính PC của bạn phục vụ, qua Tailscale của bạn. Không cần
App Store, máy Mac hay tài khoản Apple Developer.

**Chuẩn bị Tailscale (miễn phí):**

1. Cài [Tailscale](https://tailscale.com/download) trên PC và iPhone, đăng nhập cùng một tài khoản
   Tailscale của bạn.
2. Trong trang quản trị Tailscale → DNS: bật **MagicDNS** và **HTTPS Certificates**.
3. Đặt cho PC một tên máy trung tính (không chứa tên thật). Tên này hiện trong log chứng chỉ công khai.

**Ghép iPhone:**

1. Trên PC: Settings → **Truy cập từ iPhone** → bật. App tự chạy `tailscale serve` và báo trạng thái
   kèm gợi ý sửa nếu thiếu gì.
2. Bấm **Ghép iPhone**: PC hiện địa chỉ, mã QR và một mã 8 ký tự (dùng một lần, hết hạn sau 5 phút).
3. Trên iPhone: quét QR, mở bằng Safari → nút Chia sẻ → **Thêm vào MH chính**.
4. Mở Jarvis từ màn hình chính (không phải trong Safari), nhập mã, rồi tạo passkey bằng Face ID khi
   được hỏi.

**Chế độ Internet (tuỳ chọn):** bật **Mở ra Internet** nếu muốn dùng iPhone mà không bật VPN Tailscale
trên điện thoại. Jarvis đưa cổng 8443 lên Tailscale Funnel; mỗi phiên phải mở khoá bằng Face ID.
Jarvis không đụng tới cổng 443 hay cổng nào đang dùng cho việc khác.

Muốn thu hồi quyền một máy, bấm **Huỷ ghép** trong danh sách thiết bị trên PC.

## Tuỳ chọn: Giao dịch (Trading)

Hãy bắt đầu ở **PAPER**: mua thử bằng số dư ảo, không cần key. Khi đã quen mới chuyển sang **LIVE**.

- Jarvis chỉ mua spot BTC, PAXG, XAUT bằng USDT trên Binance và OKX. Không bán, không futures, không
  rút tiền.
- Jarvis không bao giờ tự đặt lệnh. Lệnh thật cần bạn bấm «Xác nhận mua» và bấm thêm trong hộp thoại
  của Windows (hoặc Face ID nếu đặt từ iPhone).
- Tạo API key trên sàn bằng tài khoản của bạn: bật đọc và giao dịch spot, **tắt quyền rút tiền** (key
  có quyền rút bị từ chối), nên giới hạn theo IP nhà bạn. Key được lưu trong kho khoá của Windows trên
  máy bạn.
- Hướng dẫn từng bước tạo key nằm ngay trong app: **Cài đặt → Giao dịch → Hướng dẫn giao dịch tiền
  thật**.

Jarvis chỉ hiển thị dữ liệu và làm theo quy tắc bạn tự đặt. Đây không phải lời khuyên đầu tư.

## Cập nhật, dữ liệu và gỡ cài đặt

- **Cập nhật**: Jarvis tự kiểm tra bản mới trên trang Releases khi mở, rồi cài khi bạn thoát app hoặc
  bấm cài ngay. Mỗi bản đều có chữ ký, app từ chối bản không khớp chữ ký. Phiên bản hiện tại xem ở
  Settings → Giới thiệu.
- **Dữ liệu**: nằm trong `%APPDATA%\Jarvis` (database, log ở `logs\host.log`). Key sàn và khoá bí mật
  nằm trong kho khoá của Windows. Không có gì được gửi lên cloud.
- **Gỡ cài đặt**: Windows Settings → Apps → Jarvis → Uninstall. Muốn xoá sạch, xoá thêm thư mục
  `%APPDATA%\Jarvis`. Nếu đã bật Truy cập từ iPhone, tắt nó trước khi gỡ để Jarvis gỡ
  `tailscale serve` / Funnel khỏi máy.

## Sự cố thường gặp

| Hiện tượng | Cách xử lý |
| --- | --- |
| "The Claude Code CLI (claude) was not found on PATH" | Cài Claude Code, chạy `claude` một lần để đăng nhập, rồi khởi động lại Jarvis |
| Chat báo hết lượt hoặc bị giới hạn | Đã dùng hết quota gói Claude; chờ quota hồi hoặc nâng gói |
| SmartScreen chặn bộ cài | Bấm More info → Run anyway |
| "the install is broken. Reinstall Jarvis" | Tải lại bộ cài mới nhất và cài đè; dữ liệu vẫn giữ |
| Lịch hẹn, tin tức không chạy | Chúng chỉ chạy khi Jarvis đang mở (kể cả dưới khay), không chạy khi máy ngủ hoặc tắt |
| Truy cập từ iPhone báo lỗi Tailscale | Làm theo gợi ý trong Settings: Tailscale đang chạy và đã đăng nhập, MagicDNS và HTTPS Certificates đã bật, cổng không bị app khác dùng |
| iPhone báo mã ghép sai hoặc hết hạn | Mã chỉ sống 5 phút và dùng một lần; bấm Ghép iPhone lại để lấy mã mới |
| iPhone đòi tạo passkey nhưng không được | Passkey phải tạo trong 15 phút sau khi ghép; quá hạn thì Huỷ ghép và ghép lại |
| Đã ghép trong Safari nhưng mở từ màn hình chính lại hỏi mã | iOS tách dữ liệu Safari và web app; luôn ghép từ biểu tượng trên màn hình chính |

Vẫn kẹt thì gửi kèm file `%APPDATA%\Jarvis\logs\host.log` khi hỏi. File này không chứa key hay chữ ký.

## Về repo này

Repo này chỉ chứa bộ cài và manifest cập nhật (`latest.json`). Mỗi release gồm bộ cài Windows, chữ ký
updater (`.sig`) và `latest.json`. App đã cài kiểm tra
`https://github.com/devTah/jarvis-releases/releases/latest/download/latest.json` để cập nhật và chỉ cài
bản được ký bằng khoá updater của Jarvis. Mã nguồn không nằm ở đây.
