---
name: open-motion-techniques
description: >
  Chưng cất kỹ thuật chuyển động từ OpenMotion (Yuan-ManX/open-motion, MIT), áp dụng cho pipeline
  Remotion của Điểm Tin Công Nghệ: Motion Critique — chấm chuyển động 4 chiều
  Accessibility/Performance/Aesthetic/Consistency với cổng cứng nhấp nháy dưới 3 lần/giây;
  Variation Engine — bảng trục biến thể easing/duration/intensity/direction/origin/stagger;
  Motion Storytelling — ánh xạ cấu trúc 5 hồi Freytag sang đường cong easing/cường độ.
  Use when designing or reviewing motion for a channel template, scoring a demo's motion in
  TEMPLATE.md, defining template variants, or structuring a story-form video.
license: MIT
metadata:
  author: Distilled from Yuan-ManX/open-motion for Điểm Tin Công Nghệ
  version: "1.0.0"
---

# OpenMotion Techniques (bản chưng cất cho pipeline Remotion)

Skill này là **bản chưng cất kỹ thuật** viết riêng cho pipeline Remotion của kênh Điểm Tin Công
Nghệ, rút ra từ dự án OpenMotion (`github.com/Yuan-ManX/open-motion`, MIT — xem SOURCE.md và
LICENSE trong thư mục này). Đây **không phải** tài liệu gốc của OpenMotion và **không kèm
runtime** của nó: OpenMotion là một codebase TypeScript độc lập, kênh chỉ mượn các khung tư duy
chuyển động dưới đây và áp vào hệ Remotion + PageBlock + TEMPLATE.md sẵn có.

Ba kỹ thuật đầu là **chuẩn đã duyệt áp dụng** cho các đợt template của kênh (quyết định
2026-11-26). Hai khung cuối là **tham khảo**, chưa phải chuẩn bắt buộc.

## 1. Motion Critique — chấm chuyển động 4 chiều (QC layer)

Chạy lớp chấm này **bên cạnh** các cổng QC hiện có (stills chống lỗi dàn chữ flex dọc,
freeze-detect đoạn tĩnh ≥0,5s không chủ đích, ffprobe phân giải) — nó bổ sung, không thay thế.

Chấm mỗi demo/template theo 4 chiều, thang 1–5, kèm một dòng nhận xét cho mỗi chiều:

| Chiều | Nhìn vào cái gì |
|---|---|
| **Accessibility** | Nhấp nháy/strobe, độ tương phản của chữ đang chuyển động, chuyển động lớn gây khó chịu, có đường thoát thị giác (điểm dừng rõ) hay không |
| **Performance** | Chuyển động chỉ dùng transform/opacity, không giật frame, không layout thrash; render đúng ngân sách thời gian |
| **Aesthetic** | Easing có chủ đích (không linear mặc định), nhịp vào–giữ–ra cân đối, chuyển động phục vụ nội dung chứ không trang trí thừa |
| **Consistency** | Cùng một họ chuyển động trong toàn template và khớp ngôn ngữ chuyển động của kênh (cùng họ easing, cùng quy ước hướng/stagger) |

**Cổng cứng (hard gate) — thuộc chiều Accessibility:** mọi hiệu ứng nhấp nháy/strobe phải
**dưới 3 lần nhấp nháy mỗi giây**. Vi phạm = lỗi QC, phải sửa rồi render lại, không ép qua —
ngang hàng với cổng flex-dọc.

**Cách ghi vào TEMPLATE.md** — thêm một mục cho mỗi template/demo:

```markdown
### Motion Critique — <tên template>
| Chiều | Điểm (1–5) | Nhận xét |
|---|---|---|
| Accessibility | | (ghi rõ tần suất nhấp nháy cao nhất nếu có hiệu ứng strobe) |
| Performance | | |
| Aesthetic | | |
| Consistency | | |
```

Ba chiều Performance/Aesthetic/Consistency là điểm đánh giá để ghi nhận và cải thiện dần;
chỉ mục nhấp nháy của Accessibility là cổng chặn.

## 2. Variation Engine — bảng trục biến thể

Khi một template cần biến thể (theo mảng tin, theo ngôn ngữ, theo mức độ nóng), **không chỉnh
tay tuỳ tiện**: khai biến thể bằng 6 trục dưới đây và ghi giá trị đã chọn vào config của
template (cạnh các preset sẵn có) để biến thể tái lập được.

| Trục | Ý nghĩa | Ví dụ giá trị |
|---|---|---|
| `easing` | Họ đường cong vào/ra | `easeOutCubic`, `easeInOutQuart`, spring damping 1.0 / 0.8 / 0.5 |
| `duration` | Hệ số thời lượng so với bản gốc | `0.85×`, `1.0×`, `1.15×` |
| `intensity` | Biên độ chuyển động (quãng đường, độ phóng) | `0.6` (dịu), `1.0` (chuẩn), `1.4` (mạnh) |
| `direction` | Hướng chuyển động chủ đạo | `up`, `down`, `left`, `right`, `radial` |
| `origin` | Điểm neo xuất phát của chuyển động | `center`, `bottom-left`, `headline` |
| `stagger` | Độ trễ giữa các phần tử liên tiếp | `40ms`, `70ms`, `120ms` |

Quy ước ghi trong config: một biến thể là một preset đặt tên, liệt kê đủ 6 trục; thiếu trục nào
thì ghi rõ `inherit` (kế thừa bản gốc) thay vì bỏ trống.

## 3. Motion Storytelling — ánh xạ Freytag 5 hồi

Áp cho template **dạng kể chuyện/diễn biến**: Timeline, Debate, Top N có leo hạng, Data Story
có cao trào số liệu, video giải thích có cấu trúc mở–đỉnh–kết.

Ánh xạ 5 hồi sang đường cong easing/cường độ theo đoạn:

| Hồi | Vai trò trong video | Cường độ | Easing chủ đạo |
|---|---|---|---|
| 1. Mở (Exposition) | Đặt bối cảnh, kicker + tiêu đề | Thấp, ổn định | `easeOut` nhẹ, stagger rộng |
| 2. Phát triển (Rising) | Dồn dữ kiện, nhịp nhanh dần | Tăng đều | `easeInOut`, stagger hẹp dần |
| 3. Đỉnh (Climax) | Con số/sự kiện chính xuất hiện | Cao nhất | Vào nhanh `easeOut` mạnh, giữ khung ổn định tại giá trị đỉnh |
| 4. Lắng (Falling) | Hệ quả, đối chiếu, giải thích | Giảm dần | `easeOut` dài, chuyển động chậm lại |
| 5. Kết (Resolution) | Chốt ý, recap, end card | Thấp, tĩnh | Gần như tĩnh, chỉ còn chuyển động tối thiểu |

**Khi nào KHÔNG ép:** template tin nhanh (News Flash, Deal Alert, Security Alert dạng cảnh
báo ngắn) không có cấu trúc truyện — giữ nhịp phẳng, đều, ưu tiên tốc độ đọc; ghi trong
TEMPLATE.md là "không áp Freytag — dạng tin nhanh" để lần sau không phải tranh luận lại.

## 4. Khung tham khảo — Motion DNA (chưa phải chuẩn bắt buộc)

Khi cần so sánh hai chuyển động (ví dụ demo mới so với mẫu tham chiếu), mô tả mỗi chuyển động
bằng một "dấu vân" gồm ba thành phần: **họ easing + nhịp timing (duration/stagger) + kiểu
transform (translate/scale/rotate và biên độ)**. Hai chuyển động cùng dấu vân thì được coi là
cùng họ. Dùng khi phân tích video tham chiếu và khi muốn lai hai kiểu chuyển động mà vẫn giữ
tính nhất quán. Chưa có cổng hay điểm số đi kèm — chỉ là ngôn ngữ mô tả chung.

## 5. Khung tham khảo — Motion Auto-Fix cho truy cập (chưa phải chuẩn bắt buộc)

Danh sách tự kiểm nhanh khi một demo bị chấm Accessibility thấp:

- Giảm tần suất/biên độ mọi nhấp nháy cho tới khi dưới ngưỡng 3 lần/giây (đây là phần bắt buộc
  — xem cổng cứng ở mục 1).
- Với chuyển động lớn (parallax, zoom mạnh, trượt dài): cân nhắc biến thể `reduced` — giảm
  `intensity` xuống ≤0.5 và bỏ chuyển động nền — theo tinh thần `prefers-reduced-motion`.
- Chữ đang chuyển động vẫn phải đọc được: không để chữ vừa chạy vừa là nơi chứa thông tin duy
  nhất; thông tin chính phải xuất hiện ở trạng thái tĩnh ít nhất một nhịp giữ.

## Ghi nguồn

Mọi template áp dụng các kỹ thuật trên ghi trong TEMPLATE.md một dòng:
"theo OpenMotion (Yuan-ManX/open-motion, MIT)".
