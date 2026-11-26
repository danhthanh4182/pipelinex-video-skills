# Case 2026-11-25 — Signal news short (BT-383)

- Bài gốc: https://news.danhthanh.dev/bai/signal-chan-ai-agent-doc-trom-tin-nhan-rieng-siri-va-gemini-0d76gs (BT-383, nguồn The Hacker News)
- Định dạng: dọc 9:16, 3 đoạn × 10s = 30s, MC studio (đoạn 1+3) + B-roll minh họa (đoạn 2), nối bằng resume_from_snapshot_id.
- Prompt: mẫu 6 phần, mô tả MC dùng nguyên văn ở đoạn 1 và 3; đoạn 2 cấm tuyệt đối chữ đọc được trên màn hình điện thoại (chỉ bong bóng chat trừu tượng).
- Giọng: KHÔNG dùng thoại trong khung hình. Lồng TTS hậu kỳ bằng VieNeu-TTS v3 Turbo (SDK vieneu 3.8.5, chạy ONNX trên CPU tại ~/workspace/vieneu-venv), giọng preset "Mai Anh" (Nữ · Bắc · tin tức), 48 kHz. Ba câu lời dẫn ra 9,7 / 9,8 / 9,1 giây — đều gọn trong đoạn 10s, không phải cắt chữ.
- Kết quả: khung hình kiểm chứng đạt — MC nhất quán hai đoạn (snapshot chaining giữ mặt/trang phục/studio), đoạn 2 đúng nhịp quét → khiên/khóa, không logo lạ, không chữ cháy. Điểm nối 10s/20s sạch.
- Độ lệch nhẹ: vòng quét ở đoạn 2 ngả đỏ-cam (kịch bản không quy định màu); miệng MC hơi mở ở vài khung giữa đoạn (đang cử chỉ) — chấp nhận được vì giọng là TTS lồng ngoài.
- Bài học: (1) Với video tin tức, tách giọng TTS khỏi khung hình giúp tránh rủi ro khẩu hình và dùng được giọng bản ngữ chất lượng cao (VieNeu) thay giọng mặc định của model video. (2) list_preset_voices() trả nhãn mô tả đầy đủ ("⭐ Mai Anh — Nữ · Bắc · Phong cách tin tức") — khi gọi infer cứ truyền tên ngắn "Mai Anh". (3) Âm thanh/chuyển động vẫn phải người dùng nghiệm thu cuối.
- File: workspace/prompt-experiments/2026-11-25/signal-chan-ai-agent-full.mp4 (+ seg1/2/3, signal-vo1/2/3.wav). Đã ghi vào space san-xuat-video: package id=1, video id=2 (khâu Kiểm duyệt).

## Addendum — v2 (silent presenter) and v3 (user prompt + Remotion closing)
- v2: user flagged lip-sync mismatch (external VO can never sync). Segments 1/3 regenerated with a hard silent-presenter constraint (lips closed, folded hands, listening nods only); same VieNeu track. File: signal-chan-ai-agent-full-v2.mp4 (30s). User reaction: amused that the MC now says nothing at all — the talking-head vs narration trade-off is real; there is no lip-sync tool on this VM (needs GPU).
- v3: the user supplied his own finalized 3-scene prompt (speaking anchor, kinetic text, on-screen labels/checklist) and asked to also use the Remotion skills. Segments 1–2 generated VERBATIM from his prompt (snapshot chain): result is more dynamic; kinetic headline rendered with correct Vietnamese diacritics; toggle panels match the brief; known defects — the model's auto-captions garble one phrase ("AI Đa thắng" for "AI đọc thẳng") and small background print is noisy/wrong-year. Segment 3 could not be generated as written (tool refused); the user delegated the fix ("Em chỉnh hộ anh đi").
- Closing built in Remotion 4.0.547 (project ~/workspace/remotion-signal): scenes 1–2 pass through with their own model audio; scene 3 (13s) = v2 silent anchor stretched (playbackRate 300/390) + new VieNeu "Mai Anh" closing VO (11.04s, his exact closing line) + real-text overlays: red badge "macOS: Chưa chặn tự động", staggered 3-item checklist, hand-timed captions (Caption JSON), navy brand end card (Noto Serif wordmark as real text). Output signal-chan-ai-agent-full-v3.mp4: 33.0s, 720×1280, H.264+AAC, 12.2MB; stills verified at frames 660/780/960.
- Remotion lessons from this build: (1) @remotion/google-fonts fetches at render time and failed here (fonts.gstatic.com SSL error through the egress proxy) — self-host the woff2 subsets (vietnamese + latin) in public/fonts and load via FontFace + delayRender/continueRender; (2) in 4.0.547 the API is continueRender, not continueInBackground; (3) `npx remotion render --frames=a,b,c` produces verification stills cheaply before a full render.

## Addendum — v4 (user feedback round, 2026-11-25)
- User verdict on v3: opening MC camera angle wrong; later segments should have no MC at all.
- Segment 1 regenerated with an explicit straight-on fix (front-facing, eye level, centered, direct lens eye contact, headroom): same anchor, angle corrected, kinetic text still clean; model even added a "TIN MỚI" lower-third with Siri/Gemini chips. File: signal-talk-seg1-front.mp4.
- Closing rebuilt in Remotion WITHOUT any presenter: animated navy graphic background (dot grid, circuit traces, shield+padlock outline, drifting glow, scan sweep) + badge + checklist + captions + end card, VieNeu closing VO unchanged.
- v4 output: signal-chan-ai-agent-full-v4.mp4 — 33.0s, 720×1280, H.264+AAC, 11.6MB; stills verified (front frames + frames2 660/780/960).
- Process lesson: when the user critiques a generated presenter's ANGLE, regenerate with explicit camera language (front-facing / eye level / centered / eye contact / headroom) rather than repeating the same prompt.

## Addendum v5 (2026-11-25) — skill-driven closing upgrade

- Applied the newly installed Motion Skills to the Remotion closing: caption-animation (Whisper word-timed captions), kinetic-typography (mask-reveal end card, easeOutExpo), lower-thirds (backing + safe-area rules).
- Whisper pipeline (verified on this VM): @remotion/install-whisper-cpp 4.0.547, whisper.cpp 1.5.5, model "small"; gotchas: transcribe() needs whisperCppVersion AND an absolute inputPath (child runs with cwd=whisperPath); toCaptions takes {whisperCppOutput}. DTW gives subword tokens — merged into words by leading-space rule, then aligned 1:1 to the known script (35 words, timings real, text exact). createTikTokStyleCaptions paginates by pause gaps (made ONE page of 35 words on continuous speech) and its tokens use fromMs/toMs — paginated manually instead (<=4 words/page, break on sentence end or >400ms pause) into src/closing-pages.json, shared by the composition and the sidecar SRT.
- v5: signal-chan-ai-agent-full-v5.mp4 (33.0s, 720x1280, 11.7MB) + signal-chan-ai-agent-full-v5.srt (9 cues, +20s offset). Stills verified: active word gold at the sampled frames, checklist/badge fade out before the end card.

## Style pilot (2026-11-25) — kinetic explainer format, navy/gold

- At the user's direction, replicated the format of a reference TikTok (@diepykien, 4:08 listicle: black + grid, single orange accent, kinetic type with marker highlights, mock chat UI, numbered chapters) rebranded to the channel's navy/gold, using the Signal article and a ~57s short format.
- Production: script written first (7 sections, verified claims only) -> VieNeu voice "Minh Duc" (male, North, news style) per section -> Whisper word timings per section (same pipeline as v5; alignment needed mis-hearing split/join tables: "20/11," -> 20/thang/11, "AIIGN" -> AI agent, "sinh hon" -> Signal) -> Remotion composition "SignalStyle" in ~/workspace/remotion-signal (grid bg, header labels, ghost chapter numbers, gold highlight wipes, chat/toggle/scan/checklist furniture triggered from word timings, gold progress bar, brand end card).
- Verified via stills at 8 frames; fixed header label/lockup overlap (lockup moved bottom-right) and end-card caption ghosting (captions fade before the card). Output: signal-style-pilot-v1.mp4, 56.7s, 720x1280, 4.3MB. Logged in the video space as a new video at review stage.

## Style pilot v2 (2026-11-25) — illustrations added per user feedback

- User verdict on v1: text system OK, but the pilot lacked illustrative imagery with animation. Fix: kept the kinetic type untouched, added an animated illustration card to 5 of 7 sections — the article's REAL cover (credited "Ảnh: The Hacker News") for the event section, and 4 AI-generated illustrations in one consistent navy/circuit style (labelled "Ảnh minh họa" on-card per the channel's image rules) for iOS/Android/macOS/stakes. Card animation: spring entrance + continuous Ken Burns zoom/drift + periodic light sweep.
- Output: signal-style-pilot-v2.mp4, 56.7s, 720x1280, 8.9MB; space video id=3 notes updated; awaiting the user's verdict.

## Style pilot v3 (2026-11-25) — sound design + PipelineX alignment

- User asked for sound effects; in the same round he pointed at his PipelineX repo as the reference. Read from the repo (read-only): technews pack maps category tech -> style "news"; the news style sets music mood "neutral", Short hook = the single most important fact in under 12 words, structure hook + 4-5 scenes + outro, Short voice rate +10%; pack brand ground #13204F / accent #F49F40 (Studio navy/gold); Short target 45-60s; max 3 videos/day at 07:30/12:30/17:30; pictures policy = free-licence sources (Wikimedia/Openverse/Pixabay), never article images.
- v3 adds a fully synthesized audio layer (numpy, no external samples): neutral 16s loopable pad bed under the VO (-18.6 LUFS overall, peak -3.7 dB), whoosh on illustration entrances, page pops, scan beeps + block thud (hook), toggle click + lock thock (iOS), shield clang (Android), warning blip + tick ding (macOS), end-card sting. All SFX triggered from the same word timings as the visuals.
- Open deltas flagged to the user: cover image vs PipelineX free-licence picture policy; VO at natural rate vs the +10% Short rate.

## Template LOCKED (2026-11-25)

- The user approved pilot v3 and locked the format as the channel's standard "Kinetic Explainer" template. Applied into the production space: default VI voice set to VieNeu "Minh Duc" in space settings, a template record (video id=4) placed on the board with the condensed spec, and the approval recorded on the pilot's record (id=3).
- Full production guide written: ~/workspace/goals/pipelinex-video-production-and-planning/files/huong-dan-san-xuat-video-kinetic-template-v1.md.
- Process note: the space's updatevideo resets stage/voiceName when they are not passed — always include them when editing notes.

## Template as code (2026-11-25)

- At the user's request the locked format was refactored into a data-driven template: src/KineticTemplate.tsx renders any src/videos/<slug>.config.ts (types in src/kinetic-config.ts; blank skeleton src/videos/TEMPLATE.config.ts; recipe in TEMPLATE.md). The Signal video rewritten as data renders byte-identical to pilot v3 (same MD5) — the template is proven against the locked sample.
- Furniture triggers are word-based ("Block"/"khoa" toggle, "bao" shield, "Excluded" tick, "iOS"/"Android:" chips) — new scripts with different wording need the one-line findWordMs targets adjusted.

## Variants (2026-11-25)

- On the user's order ("Tạo ra nhiều biến thể khác có thể có") the template engine grew five variants, all on the same VideoCfg format, each with a rendered + still-verified demo: Long (chapter: sections, per-section music mood, progress ticks — signal-long-demo.mp4), Data (ChartCard/SpecsTable furniture in kinetic-extras.tsx; calm/upbeat/serious synthesized beds — demo-data.mp4, sample numbers announced as such in the VO), Silent (gen_silent.py synthetic timings 340ms/word + silent WAVs — signal-silent-demo.mp4), Wide 16:9 (src/KineticWide.tsx two-column renderer — signal-wide-demo.mp4).
- Tooling note: VieNeu WAVs are not 16kHz — resample copies with ffmpeg before Whisper; align_generic.mjs is the reusable aligner (transcribe() returns {transcription:[{tokens:[{text, offsets:{from,to}}]}]}, needs downloadWhisperModel + language "vi").
- EN variant deliberately not built: no EN voice engine chosen.

## Deal, English, voices-as-config, site presets (2026-11-25)

- Deal variant: PriceCard (image + struck list price + gold deal price + -% badge / green MIEN PHI + deadline urgency bar) and StepsCard in kinetic-extras.tsx; demo DealDemo with sample prices announced as sample in the VO.
- Voices are configuration: VideoCfg.voice = "vieneu:Minh Duc" | "kokoro:am_michael"; make_vo.py dispatches to engine scripts per venv. Kokoro ONNX (Apache-2.0) installed at ~/workspace/kokoro-venv, model ~/workspace/kokoro-model (kokoro-v1.0.onnx + voices-v1.0.bin from thewh1teagle releases); EN default am_michael saved in the space settings (voiceEn, max 120 chars).
- English variant SignalEN renders the full Signal story in English: EN labels/end card/lockup from cfg (lockup, endCard), mock triggers per language via cfg.triggers (lock "locked", guard "screen"); EndSection/SectionShell/ToggleCard/ScanCard gained optional props with VI defaults so existing renders are unchanged.
- Site presets (src/videos/site-presets.ts) map news.danhthanh.dev sections to template settings; the Digest variant (StoryCard: index chip + headline + summary + source) demos a multi-story roundup (DigestDemo).

## Background level fix (2026-11-25)

User: music + background SFX too loud. Engine-level fix (all variants inherit): music bed 0.30 -> 0.18 (StyleComposition global Audio + KineticTemplate SectionMusic), all SFX through SFX_SCALE 0.6 in the Sfx component. Verified: music-only window between sections -26.0 -> -39.1 dB mean; pilot re-rendered as v4: -19.72 LUFS, true peak -6.11 dB (was -18.56 / -3.70). VO untouched.

## Full demos (2026-11-25)

User asked for complete demos ("Làm đầy đủ demo các biến thể, tin tổng hợp"). DigestFull (~70s): intro + 5 REAL stories from the site's 22/11/2026 edition (Signal/THN, ruby2shell/Cloudflare Blog, Microsoft MAI/CafeBiz, Genie 4/DeepMind Blog, LinkModel/LinkModel Blog) + outro — headlines/summaries/sources are the site's own published text fetched from the homepage. DataFull: real MAI figures (96% performance, 5% cost vs Claude Opus 5.5, attributed to Microsoft in the VO). SignalSilentFull (~75s): all 7 Signal sections at reading pace. EN/Deal/Wide/Long re-rendered at the new audio levels. Alignment lessons: align_generic joins/splits act on the WHISPER side (joins merge consecutive whisper tokens by normalized text; splits expand one whisper token); script tokenizer splits "5.5" into "5"+".5" — post-merge digit+".x" word pairs in the output JSON; compact date forms ("22/11,") in script text match Whisper's rendering and display fine.

## Packaged as a skill (2026-11-25)

The whole production system is now the custom skill san_xuat_video_kinetic (~/workspace/custom-skills/san_xuat_video_kinetic/: skill.yaml + SKILL.md ordered by workflow + references/can-moc-tu.md, the Whisper alignment cookbook with the garble table and joins/splits patterns). Verified present in the skill catalog via skill_search. The space template record (video id=4) now names it as the official process for the San xuat video space.
