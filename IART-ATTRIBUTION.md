# Attribution — iart-ai skill packs trong thư viện custom-skills

Ghi nhận ngày 26/11/2026 (đợt build bộ template video của kênh), đối chiếu
với hai bản phân tích trong
`~/workspace/goals/pipelinex-video-production-and-planning/files/`
(`phan-tich-template-remotion-hyperframes-2026-11-26.md` và
`phan-tich-nguon-template-mien-phi-bo-sung-2026-11-26.md`).

## Nguồn

- Tổ chức: **iart-ai** — https://github.com/iart-ai
- Bản chất: "skill packs" (tài liệu SKILL.md + references dạy kỹ thuật
  motion graphics cho AI agent), không phải thư viện component.
- Giấy phép đã kiểm chứng bằng cách đọc file LICENSE thật của từng repo
  trong lượt phân tích 26/11/2026: phần lớn **MIT**, riêng
  `awesome-motion-skills` là **CC0 1.0**.

## Pack ĐÃ CÓ trong thư viện này (đối chiếu 26/11/2026)

| Repo iart-ai (giấy phép) | Skill cục bộ tương ứng |
|---|---|
| data-animation-skills (MIT) | `chart-animation` (gồm references/bar-chart-race.md + data-pipeline.md), `animated-infographic`, `presentation-video` |
| kinetic-typography-skills (MIT) | `kinetic-typography` |
| motion-design-skills (MIT) — 9/9 skill | `animation-principles`, `beat-sync-editing`, `color-motion`, `logo-animation`, `motion-background`, `shot-composition`, `after-effects`, `remotion-video`, `motion-art-direction` |
| map-animation-skills (MIT) | `map-animation` |
| explainer-video-skills (MIT) — 5/5 skill | `explainer-video`, `diagram-animation`, `isometric-animation`, `whiteboard-animation`, `wrapped-video` |
| tiktok-video-skills (MIT) | `short-form-video` (bản tương ứng cục bộ) |
| lower-thirds-skills (MIT) | `lower-thirds`, `lower-thirds-tiktok` |
| text-message-video (MIT) | `text-message-animation` |
| youtube-video-skills (MIT) | `youtube-intro-outro` (bản tương ứng một phần) |

Kết luận kiểm kê: **mọi pack iart thuộc phạm vi kênh đều đã có sẵn** trong
thư viện — đợt build template 26/11/2026 không thiếu pack nào để vận dụng.

## Pack KHÔNG lấy — kèm lý do

- **generative-illustration-skills**: repo **không có file LICENSE** →
  mặc định giữ mọi quyền, tuyệt đối không dùng (đã kiểm chứng vắng mặt
  trong thư viện này).
- Các pack ngoài phạm vi kênh / khác pipeline (theo bản phân tích):
  ad-video, ecommerce-video, freelance-motion, web-animation,
  webgl-animation, manim (pipeline Python riêng), b-roll, talking-head —
  ghi nhận tồn tại, không cài.
- `awesome-motion-skills` (CC0): chỉ là danh mục liên kết — dùng làm mục
  lục tra cứu khi cần tìm nguồn mới, không phải nội dung để cài.

## Cách vận dụng trong project video

Kỹ thuật từ các pack này đi vào bộ template kênh qua cài đặt lại theo
idiom project (frame-driven, PageBlock, font kênh) — chi tiết từng mẫu
ghi trong `~/workspace/remotion-signal/TEMPLATE.md` và
`~/workspace/remotion-signal/VENDORED.md`. Nổi bật nhất:
`chart-animation/references/bar-chart-race.md` → cơ chế đua xếp hạng của
mẫu Top N (BarRaceCard).
