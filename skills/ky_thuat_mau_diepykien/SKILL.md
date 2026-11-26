# Kỹ thuật mẫu tham chiếu @diepykien — TÀI LIỆU HOÁ, CHƯA ÁP DỤNG

> Trạng thái: ban đầu (25/11/2026 22:21) skill này CHỈ là tài liệu tham chiếu
> theo đính chính phạm vi của người dùng. Đến 22:23 cùng ngày người dùng ra
> lệnh "có thể áp dụng" — năm yếu tố đã được tích hợp vào template Kinetic
> dạng opt-in (mặc định tắt, không đổi video cũ): furniture `strike`,
> furniture `verdict`, furniture `meter`, header tiến độ "MỤC x/N", và
> `punch` zoom-punch; highlight từ khóa chuyển sang quét lũy tiến theo
> khoảng đọc của từ. Demo đối chiếu: composition `DemoRef`. Các yếu tố còn
> lại trong tài liệu này vẫn ở trạng thái tham chiếu, chờ lệnh riêng.
>
> Mẫu gốc: video TikTok của @diepykien ("8 nguyên tắc tối thượng khi nhắn tin
> tán gái") — chính là video đã truyền cảm hứng cho template Kinetic Explainer
> của kênh Điểm Tin Công Nghệ. File mẫu lưu tại
> `~/workspace/user/media_library/video/ea/eaffcb34f149b81221cb7f5db6bbc298851e547519c153b1af10e207240eb98f.mp4`
> (576×1024, 30fps, 248,4s, H.264 + AAC).
> Bản phân tích đối chiếu đầy đủ:
> `~/workspace/goals/pipelinex-video-production-and-planning/files/phan-tich-mau-diepykien-vs-template-kinetic-2026-11-25.md`.
> Mã tham chiếu (chưa tích hợp) cho hai thiết bị đáng giá nhất nằm ở
> `references/component-tham-chieu.md` trong thư mục skill này.

## 1. Hệ thống hình ảnh của mẫu

- Một sân khấu duy nhất suốt video: nền đen-xám rất tối + lưới blueprint mờ,
  KHÔNG đổi cảnh nền; mọi thay đổi là phần tử hiện/biến trên cùng sân khấu
  (dò chuyển cảnh tự động chỉ bắt được 2 điểm cắt cứng: ~1,8s và ~228,4s).
- Đúng MỘT màu nhấn: cam rực (gần #FF6B1A). Trắng cho chữ chính, xám cho chữ
  phụ/mờ. Bong bóng chat tím là màu phụ duy nhất, chỉ trong mock chat.
- Font sans đậm, uppercase cho câu lệnh chính; cỡ chữ phân tầng rõ: câu chính
  rất lớn, câu phụ nhỏ và xám hơn hẳn.
- Avatar tròn nhỏ của kênh ở góc phải header, hiện gần như suốt video.

## 2. Cấu trúc tổng thể (248,4s)

| Đoạn | Thời lượng | Nội dung |
|---|---|---|
| Hook tĩnh | 0–5s | Hai thẻ chat nghiêng xếp lớp trên nền mờ; nhãn stamp cam nảy lên từng thẻ; tiêu đề lớn + highlight quét; cú zoom-punch chữ khổng lồ; hộp outline cam bung vào; phụ đề nhỏ |
| Neo mở đầu | 5–16s | Sân khấu lưới; thẻ lịch "THÁNG 11 / 19" lật vào (neo thời gian kiểu editorial); câu dẫn |
| 8 chương | ~16–240s | Mỗi chương ~25–30s: thẻ số chương mở đầu → 3–5 beat chữ động → 1–2 mock UI/furniture |
| Thẻ kết | ~240–248s | Avatar ảnh thật tròn lớn + tên kênh + dòng chốt + nút pill cam "THẢ TIM & FOLLOW" |

Nhịp: mỗi beat chữ 2–5s; không có khoảng chết dài; phần tử mới xuất hiện
gần như mỗi 1–2s trong các đoạn furniture.

## 3. Header tiến độ chương (cố định)

- Trái: "NGUYÊN TẮC 1/8 · PROFILE ẤN TƯỢNG" — phân số tiến độ (chương hiện
  tại / tổng số) + tên chương viết hoa, cỡ nhỏ, màu trắng/xám.
- Phải: avatar tròn của kênh.
- Header xuất hiện từ sau hook và giữ nguyên vị trí suốt video; chỉ nội dung
  phân số + tên chương thay đổi.
- Bên trong chương còn có kicker phụ kiểu "— VÀ CUỐI CÙNG", "THỬ LẬT NGƯỢC
  LẠI" (chữ cam nhỏ, có gạch ngang dẫn) để đánh dấu tiểu đoạn.

## 4. Thẻ số chương

- Số chương khổng lồ (05/06/07/08) màu trắng, chiếm ~1/4 chiều cao khung.
- Kicker cam phía trên: "— NGUYÊN TẮC THỨ NĂM" (chữ nhỏ, có dấu gạch dẫn).
- Tiêu đề chương cam, uppercase, dưới số.
- Thẻ số là một beat riêng mở chương, giữ ~2–3s trước khi vào nội dung.

## 5. Chữ động (kinetic typography)

- Đơn vị hiện chữ: cụm từ/câu ngắn theo nhịp đọc, KHÔNG gõ từng ký tự
  (đã kiểm chứng ở cửa sổ 2fps của hook và cửa sổ 1fps cuối video — không
  có hiệu ứng typewriter ký tự).
- Highlight marker: nền cam + chữ đen cho cụm khóa, quét LŨY TIẾN theo từng
  từ trong cụm đúng lúc đọc tới (không phủ cả cụm cùng lúc). Đây là điểm mẫu
  làm tốt hơn template hiện tại của kênh (wipe cả cụm).
- Hai tầng nhấn: (a) block cam nền/chữ đen cho cụm khóa nhất; (b) chữ cam
  trơn cho từ nhấn phụ ngay trong dòng trắng.
- Dòng phụ: chữ xám, nhỏ hơn, thường là mệnh đề giải thích đi sau câu chính.
- Zoom-punch chuyển beat: một từ/cụm phóng khổng lồ cắt khung trong ~0,3–0,5s
  rồi cắt sang beat kế — dùng ở hook và các điểm nhấn lớn.

## 6. Thiết bị gạch ngang sửa sai (đặc trưng nhất)

- Trình tự: câu khẳng định hiện đầy đủ → một cụm trong câu bị gạch ngang
  (đường gạch quét trái→phải, cụm bị gạch mờ đi) → cụm ĐÚNG hiện thay thế ở
  dòng dưới dạng block nhấn.
- Ví dụ trong mẫu: "Không có nghĩa [bạn kém cỏi — gạch] → chỉ là KHÔNG HỢP
  NHAU"; "không phải bằng một tối" bị gạch khi chữ "THÁNG" lớn xuất hiện.
- Giá trị với bản tin: đây là thiết bị "sửa tin đồn / đính chính claim" tự
  nhiên nhất — rất hợp triết lý kiểm chứng của kênh. Mã tham chiếu dựng lại
  (chưa tích hợp): `references/component-tham-chieu.md`, mục StrikeLine.

## 7. Nhãn stamp

- Nhãn chữ nhỏ nền cam, chữ đen, hơi nghiêng, nảy (pop/spring) gắn lên các
  thẻ mock đúng lúc câu đọc tới từ khóa (vd "BỊ CHẶN" gắn lên từng thẻ chat).
- Kích thước nhỏ so với thẻ (khoảng 1/5 chiều rộng thẻ), đặt chồng lên mép
  trên của thẻ.

## 8. Mock UI

- Thẻ chat: hai thẻ nghiêng nhẹ (~2–3°), xếp lớp lệch nhau, nền thẻ tối,
  bong bóng tím cho tin nhắn đến, có dòng thời gian/trạng thái mờ.
- Thẻ profile MXH: avatar tròn + tên + dòng số liệu ("1,2K bạn bè") + một
  dòng có dấu ✓.
- Chồng thông báo hệ thống: 2–3 thẻ thông báo xếp chồng (icon tim + tên +
  thời gian "từ năm 2024 / từ năm 2021").
- Mock điện thoại: khung điện thoại chứa screenshot chat thật, đặt giữa
  khung hình như "bằng chứng".
- Ảnh/thumbnail thật nhỏ chèn như bằng chứng minh họa (vd ảnh sân bóng).

## 9. Checklist phán quyết (✓ / ✗)

- Các hàng hiện lần lượt theo nhịp; mỗi hàng: vòng tròn chứa ✓ (đúng — viền/
  nền cam) hoặc ✗ (sai — mờ/xám), kèm chữ; hàng đúng có viền cam nổi bật.
- Khác checklist các bước: đây là phán quyết đúng/sai, không phải trình tự.
- Ví dụ trong mẫu: "✓ Đúng lúc ĐANG VUI" / "✗ Kéo đến lúc NHẠT".
- Mã tham chiếu dựng lại (chưa tích hợp): `references/component-tham-chieu.md`,
  mục VerdictChecklist.

## 10. Thanh meter so sánh

- 3 hàng ngang, mỗi hàng: nhãn trái ("Sơ sài / Tạm ổn / Đầy đủ") + thanh
  trượt ngang có núm; hàng ở mức đúng được tô cam đầy, các hàng khác xám.
- Dùng để so sánh mức độ/chất lượng — tương đương biểu đồ nhưng "cơ học" hơn.

## 11. Thẻ kết

- Avatar ảnh thật của tác giả (tròn, lớn, giữa khung), tên kênh uppercase
  dưới avatar, một dòng chốt ngắn, nút pill cam chữ đen "THẢ TIM & FOLLOW".
- Với kênh Điểm Tin Công Nghệ: vai trò này đã do thẻ kết lockup thương hiệu
  đảm nhiệm — KHÔNG thay bằng avatar người thật (đã ghi nhận là không hợp).

## 12. Đối chiếu nhanh với template Kinetic của kênh

Đã có và sát: nền lưới + 1 màu nhấn (đã bản địa hoá navy/vàng), chữ động
theo mốc từ Whisper, thẻ số chương (ChapterCard + số ma), mock chat, thẻ kết
CTA, progress bar có vạch chương.
Chưa có (chỉ áp dụng khi có lệnh riêng): gạch-sai–thay-đúng, checklist ✓/✗,
phân số tiến độ x/N trong header, highlight quét lũy tiến trong cụm dài,
meter ngang, zoom-punch, mock profile/thông báo.
Không hợp bản tin: thẻ profile MXH kiểu tán tỉnh, avatar người thật ở thẻ
kết. Mock thông báo hệ thống chỉ đáng xét cho tin bảo mật (cảnh báo giả).

## 13. Thông số dựng lại (khi được lệnh áp dụng)

- Sân khấu 720×1280 (quy đổi từ mẫu 576×1024): header y ≈ 200–260 (trong
  vùng an toàn), thẻ số chương cỡ chữ ≈ 150–170px, câu chính 54–72px,
  dòng phụ 30–34px.
- Highlight: phủ nền theo từng từ, mỗi từ ~120–200ms; đường gạch sửa sai
  quét trong ~0,5s, cụm thay thế nảy vào sau ~0,15s bằng spring
  (damping ~13, stiffness ~210).
- Stamp: scale từ 0,6→1 + xoay nhẹ −4°, ~0,25s.
- Mọi phần tử mới phải tôn trọng vùng an toàn và chuẩn âm thanh hiện hành
  của template kênh (xem skill san_xuat_video_kinetic).
