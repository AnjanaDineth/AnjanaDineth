import { useState } from "react";

const ASCII_ART = `..............:::::::::::-::::::::::......  
.........::::::.::....:--------:::::....... 
.......:::::. ...:     .--------::::........
...::::::::.   ...=++-  :-------:::::......
..::::::---    :+%@@@%*. =-------::::::.....
.::::-----=- .-*%#+--==-+#====-----:::::....
::::---====+=...:-++*%%#=#++++===----::::...
:::---===+++*=:=*=++***=.*%#**+++===--::::..
::----==+++***+.:.:=+=. .-=#%%#**++==--:::..
:::----==+**###-  ....  -=. -+*****++=--::..
.::::--=+++=-:        .-+%:     ..:--==-::..
...::--:.         .-=+*#*:            :-::..
...:::             .-+=:               :::..
...::.                                  :...
 ....                                   ....
   .                                     ...
                                          . 
                                            `;

const DOT = ({ color }) => (
  <div style={{
    width: 12, height: 12, borderRadius: "50%",
    background: color, flexShrink: 0
  }} />
);

const Row = ({ label, value, valueColor, dots = 18 }) => (
  <div style={{ display: "flex", alignItems: "baseline", fontSize: 12, lineHeight: "2", gap: 6 }}>
    <span style={{ color: "var(--cyan)", minWidth: 110, fontSize: 11, flexShrink: 0 }}>{label}</span>
    <span style={{ color: "var(--dim)", fontSize: 10, letterSpacing: 2, overflow: "hidden", whiteSpace: "nowrap", flex: 1 }}>
      {".".repeat(dots)}
    </span>
    <span style={{ color: valueColor || "var(--text)", fontSize: 12, flexShrink: 0 }}>{value}</span>
  </div>
);

const SectionHeader = ({ title, colors }) => (
  <div style={{ display: "flex", alignItems: "center", gap: 8, marginBottom: 8 }}>
    <span style={{ color: "var(--orange)", fontSize: 11, fontWeight: 700, letterSpacing: 3, textTransform: "uppercase" }}>
      {title}
    </span>
    <div style={{ flex: 1, height: 1, background: "var(--border)" }} />
  </div>
);

export default function Neofetch() {
  const [dark, setDark] = useState(true);

  const theme = dark ? {
    "--bg": "#0d1117",
    "--panel": "#161b22",
    "--border": "#30363d",
    "--text": "#e6edf3",
    "--dim": "#8b949e",
    "--cyan": "#00f7ff",
    "--orange": "#ff9500",
    "--green": "#3fb950",
    "--pink": "#ff6b9d",
    "--yellow": "#ffd60a",
  } : {
    "--bg": "#f6f8fa",
    "--panel": "#ffffff",
    "--border": "#d0d7de",
    "--text": "#1f2328",
    "--dim": "#656d76",
    "--cyan": "#0969da",
    "--orange": "#bc4c00",
    "--green": "#1a7f37",
    "--pink": "#bf3989",
    "--yellow": "#9a6700",
  };

  const css = Object.entries(theme).map(([k, v]) => `${k}: ${v}`).join(";");

  return (
    <div style={{ background: "var(--bg)", minHeight: "100vh", display: "flex", alignItems: "center", justifyContent: "center", padding: 20, ...Object.fromEntries(Object.entries(theme).map(([k,v])=>[k,v])) }}>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;700&display=swap');
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'JetBrains Mono', monospace; }
        @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }
        .cursor { display:inline-block; width:8px; height:14px; background:var(--cyan); animation:blink 1s infinite; border-radius:1px; vertical-align:middle; margin-left:4px; }
        a { color: inherit; text-decoration: none; }
        a:hover { color: var(--cyan) !important; }
      `}</style>

      <div style={{ background: "var(--panel)", border: "1px solid var(--border)", borderRadius: 12, overflow: "hidden", maxWidth: 900, width: "100%", boxShadow: dark ? "0 16px 48px rgba(0,0,0,0.5)" : "0 8px 32px rgba(0,0,0,0.1)" }}>
        
        {/* Titlebar */}
        <div style={{ background: "var(--border)", padding: "10px 16px", display: "flex", alignItems: "center", gap: 8 }}>
          <DOT color="#ff5f57" />
          <DOT color="#febc2e" />
          <DOT color="#28c840" />
          <span style={{ flex: 1, textAlign: "center", fontSize: 12, color: "var(--dim)", marginLeft: -60 }}>
            anjana@github — bash — 80×40
          </span>
          <button
            onClick={() => setDark(!dark)}
            style={{ background: "transparent", border: "1px solid var(--border)", color: "var(--dim)", fontFamily: "inherit", fontSize: 11, padding: "3px 10px", borderRadius: 4, cursor: "pointer" }}
          >
            {dark ? "☀ light" : "🌙 dark"}
          </button>
        </div>

        {/* Terminal body */}
        <div style={{ display: "flex", padding: 24, gap: 28, alignItems: "flex-start" }}>

          {/* ASCII side */}
          <div style={{ flexShrink: 0 }}>
            <pre style={{
              fontSize: 8,
              lineHeight: 1.2,
              letterSpacing: "0.4px",
              color: "var(--cyan)",
              opacity: 0.85,
              fontFamily: "'JetBrains Mono', monospace",
              whiteSpace: "pre",
            }}>
              {ASCII_ART}
            </pre>
          </div>

          {/* Info side */}
          <div style={{ flex: 1, minWidth: 0 }}>
            <div style={{ fontSize: 17, fontWeight: 700, color: "var(--cyan)", marginBottom: 4 }}>
              anjana@AnjanaDineth
            </div>
            <div style={{ color: "var(--border)", fontSize: 12, marginBottom: 16, letterSpacing: 2 }}>
              ────────────────────────────────────
            </div>

            {/* Current Project */}
            <div style={{ marginBottom: 14 }}>
              <SectionHeader title="Current Project" />
              <Row label="Project" value="Decentralized Finance" valueColor="var(--green)" />
              <Row label="Status" value="[ actively building ]" valueColor="var(--yellow)" />
              <Row label="Goal" value="Ship fast. Learn faster." />
            </div>

            {/* Hobbies */}
            <div style={{ marginBottom: 14 }}>
              <SectionHeader title="Hobbies & Interests" />
              <Row label="Learning" value="Always. Everyday." valueColor="var(--pink)" />
              <Row label="Building" value="Products & startups" />
              <Row label="Movies" value="Sci-fi & thrillers 🎬" />
              <Row label="Exploring" value="AI, Web3, new ideas 🌐" />
              <Row label="Vibe" value="Curious by default" valueColor="var(--yellow)" />
            </div>

            {/* GitHub Stats */}
            <div style={{ marginBottom: 14 }}>
              <SectionHeader title="GitHub Stats" />
              <Row label="Profile" value="github.com/AnjanaDineth" />
              <Row label="Commits" value="[ live on your profile ]" valueColor="var(--green)" />
              <Row label="Streak" value="[ auto from streak-stats ]" valueColor="var(--pink)" />
            </div>

            {/* Social */}
            <div style={{ marginBottom: 14 }}>
              <SectionHeader title="Social Links" />
              <Row label="LinkedIn" value="linkedin.com/in/yourprofile" />
              <Row label="Twitter / X" value="@yourhandle" />
              <Row label="Email" value="your@email.com" />
            </div>

            {/* Color blocks */}
            <div style={{ display: "flex", gap: 4, marginTop: 16 }}>
              {["#ff5f57","#febc2e","#28c840","#00f7ff","#ff6b9d","#ffd60a","#bf68ff","#e6edf3"].map(c => (
                <div key={c} style={{ width: 22, height: 22, borderRadius: 3, background: c, border: "1px solid rgba(255,255,255,0.08)" }} />
              ))}
            </div>

            {/* Prompt */}
            <div style={{ fontSize: 11, color: "var(--dim)", marginTop: 18, display: "flex", alignItems: "center", gap: 6 }}>
              <span style={{ color: "var(--green)" }}>❯</span>
              <span>always building, always learning</span>
              <span className="cursor" />
            </div>
          </div>
        </div>
      </div>
    </div>
  );
}
