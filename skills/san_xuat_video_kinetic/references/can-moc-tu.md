# Căn mốc từ bằng Whisper — sổ tay sửa lỗi khớp từ

Dùng kèm skill `san_xuat_video_kinetic`, mục "Căn mốc từ bằng Whisper". Mọi mẫu ở đây đã kiểm chứng thực tế trên các video ngày 25/11/2026 (Signal VI/EN, deal, tổng hợp, dữ liệu).

## Cách align_generic.mjs hoạt động

- Whisper chép giọng thành token subword; script gộp thành từ theo quy tắc: token bắt đầu bằng khoảng trắng = từ mới, token không có khoảng trắng đầu = nối vào từ trước, dấu câu rời gắn vào từ trước.
- `splitScript` tách kịch bản thành từ, và nó chèn khoảng trắng trước mọi dấu `. , ? :` rồi gắn lại dấu câu đơn độc vào từ trước. Hệ quả: "5.5" luôn bị đếm thành HAI từ ("5" và ".5"), "22/11" giữ nguyên MỘT từ vì "/" không nằm trong nhóm dấu bị tách.
- `joins` và `splits` đều tác động lên phía Whisper sau khi gộp từ:
  - `joins: [["a","b"]]` — khi hai từ Whisper liên tiếp có dạng chuẩn hoá (thường hoá, bỏ dấu câu) bằng "a" rồi "b", chúng gộp thành một từ (nối liền không khoảng trắng), mốc kéo dài tới cuối từ thứ hai.
  - `splits: {"token": ["w1","w2"]}` — một từ Whisper có nguyên văn bằng "token" (hoặc dạng chuẩn hoá bằng khóa) được tách thành các phần, mốc chia đều theo thời lượng của từ gốc.
- Kết quả cuối: chữ hiển thị lấy từ kịch bản, mốc lấy từ phía Whisper đã sửa; hai phía phải bằng số lượng theo từng phần.

## Các mẫu sửa theo triệu chứng

### Ngày tháng: kịch bản nhiều hơn Whisper 2 từ

Triệu chứng: kịch bản "ngày 22 tháng 11:" (4 từ) — Whisper nghe "ngày 22/11," (2 từ).
Sửa: đổi văn bản căn mốc của phần đó sang dạng gọn "ngày 22/11,". Chữ hiển thị dạng gọn đọc vẫn rõ nghĩa và khớp nhịp nói thật. Áp dụng tương tự cho "ngày 2 tháng 12" → "ngày 2/12.".

### Số thập phân "5.5": kịch bản nhiều hơn Whisper 1 từ

Triệu chứng: kịch bản đếm "5" + ".5" = 2 từ — Whisper có một token "5.5".
Sửa: thêm `splits: {"5.5": ["5", ".5"]}` vào manifest của phần đó (khóa có dấu phẩy đi kèm nếu token Whisper là "5.5,"). Sau khi căn xong, chạy bước gộp hậu kỳ trên file words: cặp từ liên tiếp mà từ đầu là số nguyên và từ sau bắt đầu bằng "." thì gộp thành một từ ("5" + ".5," → "5.5,"), mốc từ đầu của từ đầu tới cuối của từ sau. Không gộp thì phụ đề hiện "5 .5" rời nhau.

### Tên riêng bị Whisper nghe tách đôi: Whisper nhiều hơn kịch bản 1 từ

Triệu chứng: "macOS" → "mac" + "OS"; "DeepMind" → "Dev" + "Mine"; "LinkModel" → "link" + "model".
Sửa: `joins` theo dạng chuẩn hoá: `[["mac","os"]]`, `[["dev","mine"]]`, `[["link","model"]]`. Chữ hiển thị vẫn là tên đúng trong kịch bản.

### Một từ bị nghe dính vào từ kề: Whisper ít hơn kịch bản 1 từ

Triệu chứng: "nhớ ứng" → token dính "nhớứng"; "trang, link" → "trangLinh"; "năm, ưu" → "năng,ưu".
Sửa: `splits` với khóa là nguyên văn token dính: `{"nhớứng": ["nhớ","ứng"]}`, `{"trangLinh": ["trang,","link"]}`, `{"năng,ưu": ["năm,","ưu"]}`. Mốc chia đều là đủ vì hai từ kề nhau nói liền.

### Từ viết tắt bị nghe thành nhiều token

Triệu chứng: "WAF" → "VCAP" + "AF"; "ruby2shell" → "Ruby" + "Toshel"; "MAI Code" → token dính "MyCode".
Sửa: viết tắt bị tách đôi thì `joins: [["vcap","af"]]`, `[["ruby","toshel"]]`; tên bị dính thành một token thì `splits: {"mycode": ["My","Code"]}`.

### Whisper bỏ hẳn một từ ngắn

Triệu chứng: "API AI" — Whisper chỉ chép "API," (giọng đọc nuốt từ thứ hai).
Sửa: chấp nhận bỏ từ đó khỏi văn bản căn mốc của phần (phụ đề thiếu một từ không nghe rõ vẫn đúng nghĩa), hoặc tách token đã có bằng splits nếu cần giữ đủ chữ. Ưu tiên trung thực với âm thanh thật: người xem nghe gì thì chữ hiện nấy.

## Bảng nghe sai thường gặp (giọng Minh Đức, model small)

| Kịch bản | Whisper nghe | Cách xử lý |
|---|---|---|
| MAI | My / mai | Không cần sửa nếu số từ khớp; chữ hiển thị lấy từ kịch bản |
| Claude | Cloud | Như trên |
| WAF | VCAP AF | joins |
| ruby2shell | Ruby Toshel | joins |
| DeepMind | Dev Mine | joins |
| macOS | mac OS | joins |
| LinkModel | link model | joins |
| 96% / 55% / 5% | giữ nguyên kèm % | Khớp tự nhiên |
| 22 tháng 11 | 22/11 | Đổi văn bản căn mốc sang dạng gọn |
| template | thêm clip (giọng đọc khác) | joins theo cặp thực tế của phần đó |

## Quy trình khi lệch từ

1. Đọc hai dòng `whisper:` và `script :` mà script in ra, xác định đúng đoạn lệch và chênh bao nhiêu từ.
2. Chọn mẫu sửa ở trên; chỉ sửa manifest (joins/splits/văn bản căn mốc), không sửa file WAV và không sửa kịch bản gốc đã duyệt.
3. Chạy lại; script dừng ở phần lệch đầu tiên nên sửa theo thứ tự từng phần.
4. Căn xong toàn bộ thì chạy gộp hậu kỳ cho số thập phân rồi mới viết cấu hình.
