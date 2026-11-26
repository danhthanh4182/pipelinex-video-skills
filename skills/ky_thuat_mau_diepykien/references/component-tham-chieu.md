# Mã tham chiếu — CHƯA TÍCH HỢP VÀO TEMPLATE ĐANG CHẠY

> Hai component dưới đây được viết sẵn trong đợt research 25/11/2026 để làm tài sản tham chiếu.
> Chúng KHÔNG nằm trong project remotion-signal và không được template Kinetic sử dụng.
> Chỉ khi có lệnh riêng của người dùng mới chép vào `src/kinetic-extras.tsx`, thêm kiểu
> `verdict` / `strike` vào `SectionCfg` trong `src/kinetic-config.ts` và nối nhánh render
> trong `KineticTemplate.tsx` (mỗi furniture một nhánh cạnh nhánh `steps`).

```tsx
// ---------- Right/wrong verdict checklist (reference study 25/11) ----------

export const VerdictChecklist: React.FC<{
  title: string;
  rows: { text: string; ok: boolean }[];
}> = ({ title, rows }) => {
  const frame = useCurrentFrame();
  const entrance = useEntrance();
  return (
    <div style={{ ...cardShell, ...entrance }}>
      {title ? (
        <div
          style={{
            color: GOLD,
            fontWeight: 800,
            fontSize: 26,
            letterSpacing: 2,
            marginBottom: 18,
          }}
        >
          {title}
        </div>
      ) : null}
      <div style={{ display: "flex", flexDirection: "column", gap: 20 }}>
        {rows.map((row, i) => {
          const p = interpolate(frame, [8 + i * 12, 21 + i * 12], [0, 1], {
            easing: Easing.bezier(0.16, 1, 0.3, 1),
            extrapolateLeft: "clamp",
            extrapolateRight: "clamp",
          });
          return (
            <div
              key={i}
              style={{
                display: "flex",
                alignItems: "center",
                gap: 16,
                opacity: p,
                transform: `translateX(${interpolate(p, [0, 1], [-22, 0])}px)`,
                border: `2px solid ${row.ok ? "rgba(242,178,53,0.55)" : "rgba(214,69,65,0.45)"}`,
                borderRadius: 14,
                padding: "13px 16px",
                background: "rgba(255,255,255,0.03)",
              }}
            >
              <span
                style={{
                  width: 44,
                  height: 44,
                  borderRadius: "50%",
                  background: row.ok ? GOLD : "#D64541",
                  color: row.ok ? INK : "#FFFFFF",
                  fontSize: 26,
                  fontWeight: 900,
                  display: "flex",
                  alignItems: "center",
                  justifyContent: "center",
                  flexShrink: 0,
                }}
              >
                {row.ok ? "✓" : "✕"}
              </span>
              <span
                style={{
                  color: row.ok ? "#FFFFFF" : "rgba(255,255,255,0.82)",
                  fontSize: 29,
                  fontWeight: 700,
                  lineHeight: 1.4,
                  textWrap: "balance",
                }}
              >
                {row.text}
              </span>
            </div>
          );
        })}
      </div>
    </div>
  );
};

// ---------- Strike-through correction device (reference study 25/11) ----------
// A claim is stated, the wrong part is struck through, and the correction
// pops in below as a gold block. Frame-driven: strike sweeps at f34–50,
// the struck words dim, the correction springs in at f54.

export const StrikeLine: React.FC<{
  lead: string;
  struck: string;
  tail?: string;
  replace: string;
}> = ({ lead, struck, tail, replace }) => {
  const frame = useCurrentFrame();
  const entrance = useEntrance();
  const strikeP = interpolate(frame, [34, 50], [0, 1], {
    easing: Easing.bezier(0.16, 1, 0.3, 1),
    extrapolateLeft: "clamp",
    extrapolateRight: "clamp",
  });
  const dim = interpolate(frame, [46, 58], [1, 0.45], {
    extrapolateLeft: "clamp",
    extrapolateRight: "clamp",
  });
  const pop = spring({ frame: frame - 54, fps: 30, config: { damping: 13, stiffness: 210, mass: 0.7 } });
  return (
    <div
      style={{
        position: "absolute",
        left: 40,
        top: 330,
        width: 573,
        ...entrance,
      }}
    >
      <div
        style={{
          fontFamily: beVietnam,
          fontSize: 44,
          fontWeight: 800,
          lineHeight: 1.35,
          color: "#FFFFFF",
        }}
      >
        {lead}{" "}
        <span style={{ position: "relative", display: "inline-block", opacity: dim }}>
          {struck}
          <span
            style={{
              position: "absolute",
              left: -4,
              right: -4,
              top: "54%",
              height: 6,
              borderRadius: 3,
              background: "#D64541",
              transform: `scaleX(${strikeP})`,
              transformOrigin: "left center",
            }}
          />
        </span>
        {tail ? <> {tail}</> : null}
      </div>
      <div
        style={{
          marginTop: 34,
          opacity: pop,
          transform: `scale(${interpolate(pop, [0, 1], [0.7, 1])})`,
          transformOrigin: "left center",
          background: GOLD,
          color: INK,
          fontWeight: 900,
          fontSize: 36,
          lineHeight: 1.3,
          padding: "16px 20px",
          borderRadius: 14,
          display: "inline-block",
        }}
      >
        {replace}
      </div>
    </div>
  );
};

```
