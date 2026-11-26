# Bộ skill video PipelineX

Bản xuất ngày 26/11/2026. Mỗi skill nằm trong một thư mục riêng dưới `skills/`, với `SKILL.md`, cấu hình hiển thị và tài nguyên đi kèm nếu có. Nội dung workflow giữ nguyên tiếng Anh. Hướng dẫn cài đặt này dùng tiếng Việt.

[![skills.sh](https://skills.sh/b/danhthanh4182/pipelinex-video-skills)](https://skills.sh/danhthanh4182/pipelinex-video-skills)

## Cài bằng Skills CLI

Chạy trong thư mục dự án để cài cả 14 skill cho Codex.

```sh
npx skills add danhthanh4182/pipelinex-video-skills --skill '*' --agent codex --yes
```

Cài riêng skill điều phối PipelineX.

```sh
npx skills add danhthanh4182/pipelinex-video-skills --skill pipelinex-video-studio --agent codex --yes
```

Xem danh sách trước khi cài hoặc kiểm tra các skill đã cài.

```sh
npx skills add danhthanh4182/pipelinex-video-skills --list
npx skills list
```

Lệnh dùng được trong PowerShell và WSL. Thêm `--global` nếu muốn cài cho mọi dự án của môi trường đang chạy. Mở dự án trong Codex và gọi `$pipelinex-video-studio` để bắt đầu. [Tài liệu Skills CLI](https://www.skills.sh/docs/cli)

## Danh sách 14 skill

| Skill | Công việc |
| --- | --- |
| `pipelinex-video-studio` | Điều phối dựng và kiểm duyệt trong PipelineX |
| `remotion-video-templates` | Dựng video bằng React và Remotion |
| `hyperframes-video-templates` | Dựng bản xem trước bằng HTML, CSS và GSAP |
| `iart-video-briefs` | Viết brief cho motion graphics và video dữ liệu |
| `direct-video-motion` | Lập storyboard và chỉ đạo chuyển động |
| `analyze-video-references` | Tách cảnh và phân tích video, ưu tiên fork Rea-Video của bạn |
| `build-video-effects` | Dựng hiệu ứng bằng EffectCraft và PixelFX |
| `generate-comfyui-video-assets` | Chuẩn bị workflow tạo tư liệu bằng ComfyUI |
| `build-3d-video-shots` | Dựng cảnh 3D bằng Three.js và Blender |
| `deliver-video-with-ffmpeg` | Chuyển mã và kiểm tra tệp video |
| `build-code-explainers` | Dựng video giải thích có lời đọc và thanh chương |
| `direct-continuous-launch-videos` | Dựng video sản phẩm với chuyển động liền mạch |
| `render-raea-video` | Thử dựng cảnh GPU bằng Raea |
| `produce-screen-demo-video` | Quay và biên tập demo bằng OpenScreen |

Gói gồm các skill và tài nguyên của chúng. Các template mã nguồn PipelineX và ứng dụng bên thứ ba dùng bản phân phối riêng.
