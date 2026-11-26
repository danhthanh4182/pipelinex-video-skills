# Bộ công cụ animation web và video

## Khi nào dùng skill này

- Dùng skill này mỗi khi xây hoặc sửa một không gian, trang web, widget hay sản phẩm video của người dùng mà cần chuyển động, hiệu ứng, trực quan hoá dữ liệu, 3D trong trình duyệt hoặc âm thanh sinh trong trình duyệt.

- Các thư viện trong bộ này đã được kiểm chứng trên GitHub ngày 2026-11-25 (đều là repo chính thức, đang bảo trì, không bị archive) và đã cài sẵn tại `~/workspace/animation-toolkit/` với package.json ghim qua npm. Khi làm dự án mới, cài các thư viện này vào dự án bằng npm thay vì viết lại hiệu ứng từ đầu.

## Thư viện đã cài và khi nào dùng

- anime.js 4.5.0 (npm `animejs`) cho animation web mượt mà theo timeline, easing và stagger. Chọn nó cho chuyển động UI và cảnh ngắn không cần vật lý.

- @react-spring/web 10.1.2 cho chuyển động UI kiểu lò xo trong dự án React. Chọn nó khi giao diện đã là React và chuyển động cần cảm giác thật theo vật lý lò xo.

- pixi.js 8.23.0 cho render 2D tốc độ cao, hệ hạt và hiệu ứng 60fps trên canvas. Chọn nó khi số lượng đối tượng vẽ lớn mà DOM không theo kịp.

- p5 2.4.0 cho nghệ thuật sinh thành và bản phác thảo sáng tạo nhanh. Chọn nó cho thử nghiệm thị giác và generative art.

- matter-js 0.20.0 cho vật lý 2D thật như rơi, nảy và va chạm. Ghép với pixi.js hoặc canvas khi cần vừa vật lý vừa render nhanh.

- d3 7.9.2 cho biểu đồ chuyển động và trực quan hoá dữ liệu. Chọn nó cho dashboard, biểu đồ trong bài tin và đồ hoạ dữ liệu.

- @motion-canvas/core và @motion-canvas/2d 3.17.2 cho animation 2D viết bằng code thay cho keyframe. Chọn nó cho video giải thích và đồ hoạ chuyển động có kịch bản.

- three 0.187.0 cho cảnh 3D chạy trong trình duyệt. Chọn nó cho sản phẩm 3D, bản đồ 3D và hiệu ứng chiều sâu trên web.

- lottie-web 5.13.0 cho phát animation After Effects xuất dạng Lottie ngay trên web. Chọn nó khi nhà thiết kế bàn giao file Lottie.

- tone 15.1.22 cho synth, beat và hiệu ứng âm thanh trong trình duyệt qua Web Audio. Chọn nó cho âm thanh tương tác và nhạc nền sinh tại client.

## Skill Remotion đi kèm

- Bộ skill chính thức của Remotion đã cài trong cùng thư mục custom skills, gồm remotion-best-practices làm router và các skill con cho tạo dự án, captions, markup, multimedia, render và studio. Khi người dùng yêu cầu làm video bằng Remotion, đọc remotion-best-practices trước rồi đi theo router của nó.

## Công cụ chưa cài và lý do

- Blender: repo GitHub là mã nguồn C++ để tự biên dịch, không phải bản cài. Máy này chưa có binary Blender và không có GPU, render 3D nặng không khả thi trong giới hạn hiện tại. Khi cần thật, tải bản portable chính thức từ blender.org và chạy headless cho cảnh nhẹ.

- RIFE (hzwer/ECCV2022-RIFE): nội suy khung hình bằng PyTorch. Máy này không có GPU nên chạy CPU rất chậm và bộ cài PyTorch nặng vài GB. Để dành cho máy có GPU.

- MusicGen qua facebookresearch/audiocraft: tạo nhạc bằng mô hình học sâu, cần GPU và tải mô hình vài GB, vượt giới hạn bộ nhớ của máy này. Khi cần nhạc nền, ưu tiên tone để sinh âm thanh trong trình duyệt hoặc dịch vụ tạo nhạc bên ngoài.

## Kỷ luật dùng bộ công cụ

- Kiểm chứng lại phiên bản và tình trạng bảo trì trên GitHub hoặc npm trước khi dùng một thư viện cho dự án quan trọng, vì phiên bản trong toolkit là ảnh chụp tại ngày cài.

- Không chạy script lạ lấy từ repo ngoài khi chưa đọc nội dung của nó. Thư viện trong toolkit chỉ được dùng qua npm package chính thức đã cài.

## Available connectors

- Use `muse.connector_search` to find other connectors and `muse.skill_search` to find related skills.

- If nothing here fits, look on the web for a maintained API or MCP server and set it up with [Custom Connectors and MCPs](/opt/muse/skills/custom-connector-setup/SKILL.md), or build a custom connector.
