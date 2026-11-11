---
marp: true
paginate: true
size: 16:9
title: Agent Anatomy
author: Agent Fight Club
style: |
  @import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500;700&display=swap');

  :root {
    --bg: hsl(43, 100%, 50%);
    --bg-hot: hsl(43, 88%, 42%);
    --bg-deep: hsl(43, 95%, 45%);
    --ink: hsl(0, 0%, 4%);
    --ink-soft: hsla(0, 0%, 4%, 0.72);
    --ink-faint: hsla(0, 0%, 4%, 0.42);
    --paper: hsl(43, 100%, 92%);
    --panel: hsla(0, 0%, 4%, 0.06);
    --panel-strong: hsla(0, 0%, 4%, 0.10);
    --line: hsl(0, 0%, 4%);
    --hot: hsl(0, 78%, 48%);
    --green: hsl(140, 65%, 32%);
    --night: hsl(0, 0%, 4%);
    --night-fg: hsl(43, 100%, 50%);
  }

  section {
    background: var(--bg);
    color: var(--ink);
    font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
    font-size: 24px;
    line-height: 1.45;
    padding: 56px 72px;
    justify-content: flex-start;
    position: relative;
  }

  /* Page numbers — terminal flavored */
  section::after {
    font-family: 'IBM Plex Mono', monospace;
    color: var(--ink);
    font-size: 12px;
    letter-spacing: 0.16em;
    opacity: 0.6;
  }

  h1 {
    font-family: 'IBM Plex Mono', monospace;
    font-weight: 700;
    font-size: 64px;
    line-height: 1.0;
    letter-spacing: -0.05em;
    color: var(--ink);
    margin: 0 0 24px 0;
    text-transform: uppercase;
  }

  h2 {
    font-family: 'IBM Plex Mono', monospace;
    font-weight: 700;
    font-size: 13px;
    letter-spacing: 0.22em;
    text-transform: uppercase;
    color: var(--ink);
    margin: 0 0 18px 0;
    border-bottom: 2px solid var(--ink);
    padding-bottom: 6px;
    display: inline-block;
  }

  h3 {
    font-family: 'IBM Plex Mono', monospace;
    font-weight: 700;
    font-size: 26px;
    color: var(--ink);
    margin: 0 0 12px 0;
    letter-spacing: -0.02em;
  }

  p { margin: 0 0 12px 0; }

  strong { color: var(--ink); font-weight: 700; }
  em { color: var(--ink-soft); font-style: normal; text-decoration: underline; text-decoration-thickness: 2px; }

  ul, ol {
    margin: 0;
    padding-left: 0;
    list-style: none;
  }

  li {
    padding: 10px 0 10px 28px;
    border-bottom: 1px dashed var(--ink);
    position: relative;
    font-size: 22px;
  }
  li:last-child { border-bottom: none; }
  li::before {
    content: '▸';
    position: absolute;
    left: 0;
    top: 8px;
    font-weight: 700;
    color: var(--ink);
  }

  code {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.88em;
    color: var(--ink);
    background: var(--panel-strong);
    padding: 1px 6px;
    border: 1px solid var(--ink);
  }

  pre {
    background: var(--night);
    color: var(--night-fg);
    border: 2px solid var(--ink);
    padding: 16px 20px;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 16px;
    line-height: 1.45;
    overflow: hidden;
    box-shadow: 6px 6px 0 var(--ink);
  }
  pre code { background: transparent; border: none; color: var(--night-fg); padding: 0; }

  blockquote {
    border: none;
    border-left: 6px solid var(--ink);
    padding: 4px 18px;
    margin: 16px 0;
    color: var(--ink);
    font-style: normal;
    font-size: 22px;
    background: var(--panel);
  }

  hr {
    border: none;
    border-top: 2px solid var(--ink);
    margin: 20px 0;
  }

  /* ---- Title slide ---- */
  section.title {
    justify-content: center;
    align-items: flex-start;
    text-align: left;
    padding: 64px 72px;
    background:
      repeating-linear-gradient(
        90deg,
        transparent 0,
        transparent 22px,
        rgba(0,0,0,0.04) 22px,
        rgba(0,0,0,0.04) 23px
      ),
      var(--bg);
  }
  section.title .chip {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 12px;
    letter-spacing: 0.32em;
    text-transform: uppercase;
    color: var(--ink);
    border: 2px solid var(--ink);
    padding: 8px 14px;
    display: inline-block;
    background: var(--bg);
    margin-bottom: 28px;
  }
  section.title .wordmark {
    font-family: 'IBM Plex Mono', monospace;
    font-weight: 700;
    font-size: 132px;
    line-height: 0.92;
    letter-spacing: -0.07em;
    color: var(--ink);
    text-transform: uppercase;
    margin: 0 0 18px 0;
  }
  section.title .wordmark .alt { color: var(--hot); }
  section.title .tagline {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 18px;
    letter-spacing: 0.22em;
    text-transform: uppercase;
    color: var(--ink);
    border-top: 2px solid var(--ink);
    padding-top: 16px;
    max-width: 920px;
  }
  section.title .meta {
    position: absolute;
    bottom: 40px;
    left: 72px;
    right: 72px;
    display: flex;
    justify-content: space-between;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 12px;
    letter-spacing: 0.22em;
    text-transform: uppercase;
    color: var(--ink);
    border-top: 1px solid var(--ink);
    padding-top: 12px;
  }
  section.title h1 { display: none; }

  /* ---- Big title / section break ---- */
  section.bigtitle {
    justify-content: center;
    align-items: flex-start;
    padding: 72px 80px;
  }
  section.bigtitle .num {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 18px;
    letter-spacing: 0.32em;
    text-transform: uppercase;
    color: var(--ink);
    border: 2px solid var(--ink);
    padding: 8px 14px;
    background: var(--bg);
    display: inline-block;
    margin-bottom: 36px;
  }
  section.bigtitle h1 {
    font-size: 110px;
    line-height: 0.95;
    letter-spacing: -0.06em;
    margin: 0;
    max-width: 1180px;
  }
  section.bigtitle h1.sm { font-size: 84px; }
  section.bigtitle .kicker {
    margin-top: 28px;
    max-width: 980px;
    font-size: 22px;
    color: var(--ink);
    border-top: 2px solid var(--ink);
    padding-top: 16px;
  }
  section.bigtitle .kicker strong { background: var(--ink); color: var(--bg); padding: 1px 6px; }
  section.bigtitle .glyph {
    position: absolute;
    top: 64px;
    right: 80px;
    font-size: 200px;
    line-height: 1;
    filter: drop-shadow(8px 8px 0 var(--ink));
  }

  /* ---- Quote / pull-line slide ---- */
  section.pull {
    justify-content: center;
    align-items: flex-start;
    padding: 80px 96px;
  }
  section.pull .line {
    font-family: 'IBM Plex Mono', monospace;
    font-weight: 700;
    font-size: 72px;
    line-height: 1.03;
    letter-spacing: -0.04em;
    max-width: 1180px;
  }
  section.pull .line .hl { background: var(--ink); color: var(--bg); padding: 0 8px; }
  section.pull .attrib {
    margin-top: 36px;
    font-size: 14px;
    letter-spacing: 0.24em;
    text-transform: uppercase;
    color: var(--ink-soft);
  }

  /* ---- Two columns ---- */
  .cols { display: grid; grid-template-columns: 1fr 1fr; gap: 28px; margin-top: 12px; }
  .cols.heavy > div {
    border: 2px solid var(--ink);
    background: var(--bg);
    padding: 24px 28px;
    box-shadow: 6px 6px 0 var(--ink);
  }

  /* ---- Three columns ---- */
  .cols3 { display: grid; grid-template-columns: repeat(3, 1fr); gap: 18px; margin-top: 12px; }
  .cols3.two { grid-template-columns: repeat(2, 1fr); gap: 28px; }
  .cols3 .card {
    border: 2px solid var(--ink);
    background: var(--bg);
    padding: 22px 22px;
    box-shadow: 6px 6px 0 var(--ink);
    display: flex;
    flex-direction: column;
    gap: 10px;
  }
  .cols3 .card .glyph { font-size: 44px; line-height: 1; }
  .cols3 .card .num {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 12px;
    letter-spacing: 0.24em;
    text-transform: uppercase;
  }
  .cols3 .card .head {
    font-family: 'IBM Plex Mono', monospace;
    font-weight: 700;
    font-size: 20px;
    text-transform: uppercase;
    letter-spacing: -0.01em;
  }
  .cols3 .card .body {
    font-size: 16px;
    color: var(--ink-soft);
    line-height: 1.4;
  }

  /* ---- Agent equation ---- */
  section.equation .eqrow {
    display: flex;
    align-items: stretch;
    gap: 18px;
    margin-top: 44px;
  }
  section.equation .eqlead {
    font-family: 'IBM Plex Mono', monospace;
    font-weight: 700;
    font-size: 56px;
    letter-spacing: -0.05em;
    text-transform: uppercase;
    display: flex;
    align-items: center;
    white-space: nowrap;
  }
  section.equation .op {
    font-family: 'IBM Plex Mono', monospace;
    font-weight: 700;
    font-size: 56px;
    display: flex;
    align-items: center;
    color: var(--ink);
  }
  section.equation .eqcard {
    flex: 1;
    border: 2px solid var(--ink);
    background: var(--bg);
    box-shadow: 8px 8px 0 var(--ink);
    padding: 26px 24px;
    display: flex;
    flex-direction: column;
    gap: 14px;
    min-height: 320px;
  }
  section.equation .eqcard .glyph { font-size: 68px; line-height: 1; }
  section.equation .eqcard .name {
    font-family: 'IBM Plex Mono', monospace;
    font-weight: 700;
    font-size: 30px;
    line-height: 1.05;
    text-transform: uppercase;
    letter-spacing: -0.03em;
    margin-top: auto;
  }
  section.equation .eqcard .name .sub {
    display: block;
    font-size: 18px;
    letter-spacing: 0.14em;
    color: var(--ink-soft);
    margin-top: 8px;
  }

  /* ---- QR / repo slide ---- */
  section.repo .split {
    display: grid;
    grid-template-columns: 340px 1fr;
    gap: 40px;
    align-items: center;
    margin-top: 24px;
  }
  section.repo .qr {
    border: 3px solid var(--ink);
    background: var(--paper);
    padding: 18px;
    box-shadow: 10px 10px 0 var(--ink);
  }
  section.repo .qr img { width: 100%; display: block; }
  section.repo .urlbox {
    background: var(--night);
    color: var(--night-fg);
    border: 3px solid var(--ink);
    box-shadow: 10px 10px 0 var(--ink);
    padding: 24px 26px;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 22px;
    word-break: break-all;
  }
  section.repo .urlbox .hdr {
    font-size: 12px;
    letter-spacing: 0.28em;
    text-transform: uppercase;
    color: var(--hot);
    margin-bottom: 14px;
  }
  section.repo .big {
    font-family: 'IBM Plex Mono', monospace;
    font-weight: 700;
    font-size: 62px;
    line-height: 0.98;
    letter-spacing: -0.05em;
    text-transform: uppercase;
    margin-bottom: 22px;
  }

  /* ---- Divider (appendix) ---- */
  section.divider {
    justify-content: center;
    align-items: center;
    text-align: center;
    background:
      repeating-linear-gradient(
        90deg,
        transparent 0,
        transparent 22px,
        rgba(0,0,0,0.04) 22px,
        rgba(0,0,0,0.04) 23px
      ),
      var(--bg);
  }
  section.divider h1 {
    font-size: 150px;
    line-height: 0.95;
    letter-spacing: -0.06em;
    margin: 0;
    border-top: 3px solid var(--ink);
    border-bottom: 3px solid var(--ink);
    padding: 18px 0;
  }
  section.divider .rule {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 13px;
    letter-spacing: 0.4em;
    text-transform: uppercase;
    color: var(--ink-soft);
    margin-top: 22px;
  }

  /* ---- Agent loop diagram ---- */
  section.loop .diagram {
    border: 3px solid var(--ink);
    background: var(--paper);
    box-shadow: 10px 10px 0 var(--ink);
    padding: 26px 32px;
    margin-top: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  section.loop .diagram img { width: 100%; display: block; }
  section.loop .beats {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
    margin-top: 22px;
  }
  section.loop .beat {
    border-left: 6px solid var(--ink);
    background: var(--panel);
    padding: 10px 16px;
    font-size: 17px;
    line-height: 1.35;
  }
  section.loop .beat .k {
    display: block;
    font-family: 'IBM Plex Mono', monospace;
    font-weight: 700;
    font-size: 11px;
    letter-spacing: 0.24em;
    text-transform: uppercase;
    margin-bottom: 3px;
  }

  /* ---- What is an Agent? ---- */
  section.whatis .lead {
    border-left: 6px solid var(--ink);
    background: var(--panel);
    padding: 12px 18px;
    font-size: 20px;
    line-height: 1.4;
    margin-bottom: 20px;
  }
  section.whatis .lead strong { background: var(--ink); color: var(--bg); padding: 1px 5px; }

  section.whatis .eq {
    display: flex;
    align-items: stretch;
    gap: 14px;
  }
  section.whatis .eq .lead-t {
    font-family: 'IBM Plex Mono', monospace;
    font-weight: 700;
    font-size: 38px;
    letter-spacing: -0.04em;
    text-transform: uppercase;
    display: flex;
    align-items: center;
    white-space: nowrap;
  }
  section.whatis .eq .op {
    font-family: 'IBM Plex Mono', monospace;
    font-weight: 700;
    font-size: 38px;
    display: flex;
    align-items: center;
  }
  section.whatis .eq .card {
    flex: 1;
    border: 2px solid var(--ink);
    box-shadow: 7px 7px 0 var(--ink);
    padding: 16px 20px;
    display: flex;
    flex-direction: column;
    gap: 6px;
  }
  section.whatis .eq .card .name {
    font-family: 'IBM Plex Mono', monospace;
    font-weight: 700;
    font-size: 26px;
    text-transform: uppercase;
    letter-spacing: -0.02em;
  }
  section.whatis .eq .card .body { font-size: 16px; line-height: 1.35; }
  section.whatis .eq .card.model { background: var(--ink); color: var(--bg); }
  section.whatis .eq .card.model .body { color: hsla(43, 100%, 90%, 0.82); }
  section.whatis .eq .card.harness { background: var(--bg); }
  section.whatis .eq .card.harness .body { color: var(--ink-soft); }

  section.whatis .rule {
    margin-top: 20px;
    border: 3px solid var(--ink);
    background: var(--paper);
    box-shadow: 8px 8px 0 var(--hot);
    padding: 14px 20px;
    text-align: center;
    font-family: 'IBM Plex Mono', monospace;
    font-weight: 700;
    font-size: 26px;
    letter-spacing: -0.02em;
  }
  section.whatis .rule .hl { background: var(--ink); color: var(--bg); padding: 0 8px; }
  section.whatis .kicker {
    margin-top: 16px;
    font-size: 17px;
    line-height: 1.4;
    color: var(--ink-soft);
    text-align: center;
  }
  section.whatis .kicker strong { color: var(--ink); }

  /* ---- Roadmap (long-term agenda) ---- */
  section.roadmap .grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px 24px;
    margin-top: 14px;
  }
  section.roadmap .item {
    display: grid;
    grid-template-columns: 42px 1fr;
    gap: 12px;
    align-items: center;
    border-bottom: 1px dashed var(--ink);
    padding: 9px 4px;
  }
  section.roadmap .item .n {
    font-family: 'IBM Plex Mono', monospace;
    font-weight: 700;
    font-size: 17px;
    text-align: center;
    padding: 2px 0;
    border: 2px solid var(--ink);
    color: var(--ink);
  }
  section.roadmap .item .t {
    font-size: 17px;
    line-height: 1.3;
  }
  section.roadmap .item .t .sub {
    display: block;
    font-size: 14px;
    color: var(--ink-soft);
  }
  section.roadmap .item.now {
    border: 2px solid var(--ink);
    border-bottom: 2px solid var(--ink);
    background: var(--ink);
    box-shadow: 6px 6px 0 var(--hot);
    padding: 12px 10px;
  }
  section.roadmap .item.now .n { background: var(--bg); color: var(--ink); border-color: var(--bg); }
  section.roadmap .item.now .t { color: var(--bg); font-weight: 700; }
  section.roadmap .item.now .t .stamp {
    display: inline-block;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.28em;
    text-transform: uppercase;
    background: var(--hot);
    color: #fff;
    padding: 2px 6px;
    margin-right: 8px;
    vertical-align: 2px;
  }

  /* ---- LLM basics ---- */
  section.llm .split {
    display: grid;
    grid-template-columns: 1.05fr 1fr;
    gap: 30px;
    margin-top: 6px;
  }

  /* nested set diagram: ML model ⊃ neural net ⊃ LLM */
  section.llm .lvl {
    border: 2px solid var(--ink);
    padding: 12px 14px;
  }
  section.llm .lvl.l1 { background: var(--panel); box-shadow: 8px 8px 0 var(--ink); }
  section.llm .lvl.l2 { background: var(--paper); margin: 10px 0 0 28px; }
  section.llm .lvl.l3 { background: var(--bg); margin: 10px 0 0 56px; box-shadow: 5px 5px 0 var(--hot); }
  section.llm .lvl.l3 .tag { font-size: 22px; }
  section.llm .lvl .tag {
    display: block;
    font-family: 'IBM Plex Mono', monospace;
    font-weight: 700;
    font-size: 19px;
    text-transform: uppercase;
    letter-spacing: -0.01em;
  }
  section.llm .lvl .def {
    display: block;
    font-size: 15px;
    line-height: 1.35;
    color: var(--ink-soft);
    margin-top: 4px;
  }

  section.llm .termbox {
    background: var(--night);
    color: var(--night-fg);
    border: 2px solid var(--ink);
    box-shadow: 6px 6px 0 var(--ink);
    padding: 14px 18px;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 17px;
    line-height: 1.5;
  }
  section.llm .termbox .hdr {
    font-size: 11px;
    letter-spacing: 0.24em;
    text-transform: uppercase;
    color: var(--hot);
    margin-bottom: 8px;
  }
  section.llm .termbox .cursor { background: var(--night-fg); color: var(--night); }
  section.llm .termbox .out { color: #fff; font-weight: 700; }

  /* text in → LLM → text out */
  section.llm .pipe {
    display: flex;
    align-items: stretch;
    gap: 8px;
    margin-top: 14px;
  }
  section.llm .pipe .box {
    flex: 1;
    border: 2px solid var(--ink);
    background: var(--bg);
    box-shadow: 4px 4px 0 var(--ink);
    padding: 10px 6px;
    text-align: center;
    font-family: 'IBM Plex Mono', monospace;
    font-weight: 700;
    font-size: 14px;
    letter-spacing: 0.12em;
    text-transform: uppercase;
  }
  section.llm .pipe .box.core { background: var(--ink); color: var(--bg); }
  section.llm .pipe .arw {
    display: flex;
    align-items: center;
    font-family: 'IBM Plex Mono', monospace;
    font-weight: 700;
    font-size: 22px;
  }

  section.llm .stateless {
    margin-top: 14px;
    border: 2px solid var(--ink);
    border-left: 8px solid var(--hot);
    background: var(--paper);
    box-shadow: 6px 6px 0 var(--ink);
    padding: 12px 16px;
    font-size: 16px;
    line-height: 1.4;
  }
  section.llm .stateless .k {
    display: block;
    font-family: 'IBM Plex Mono', monospace;
    font-weight: 700;
    font-size: 12px;
    letter-spacing: 0.24em;
    text-transform: uppercase;
    margin-bottom: 4px;
  }

  /* ---- Framed image plate (appendix diagrams) ---- */
  section.plate { padding: 40px 64px; }
  section.plate .frame {
    border: 3px solid var(--ink);
    background: var(--paper);
    box-shadow: 10px 10px 0 var(--ink);
    padding: 20px 24px;
    margin-top: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  section.plate .frame img {
    display: block;
    max-width: 100%;
    max-height: 100%;
    object-fit: contain;
  }
  section.plate.tall .frame { height: 552px; }
  section.plate.wide .frame { height: 400px; }
  section.plate .note {
    margin-top: 16px;
    border: 2px solid var(--ink);
    background: var(--bg);
    box-shadow: 6px 6px 0 var(--hot);
    padding: 12px 18px;
    font-size: 19px;
    text-align: center;
  }
  section.plate .note strong { background: var(--ink); color: var(--bg); padding: 1px 6px; }

  /* ---- Watch list ---- */
  section.watch ol {
    counter-reset: w;
    margin-top: 16px;
  }
  section.watch li {
    counter-increment: w;
    padding: 14px 16px 14px 60px;
    border: 2px solid var(--ink);
    margin-bottom: 10px;
    background: var(--bg);
    box-shadow: 4px 4px 0 var(--ink);
    font-size: 18px;
  }
  section.watch li::before {
    content: counter(w, decimal-leading-zero);
    position: absolute;
    left: 16px;
    top: 50%;
    transform: translateY(-50%);
    font-family: 'IBM Plex Mono', monospace;
    font-weight: 700;
    font-size: 22px;
    background: var(--ink);
    color: var(--bg);
    padding: 2px 8px;
  }
  section.watch.big li { font-size: 24px; padding: 22px 20px 22px 72px; }
  section.watch.big li::before { left: 20px; font-size: 26px; }

  /* ---- Closing ---- */
  section.closing {
    justify-content: center;
    align-items: center;
    text-align: center;
    background:
      repeating-linear-gradient(
        90deg,
        transparent 0,
        transparent 22px,
        rgba(0,0,0,0.04) 22px,
        rgba(0,0,0,0.04) 23px
      ),
      var(--bg);
  }
  section.closing .stamp {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 14px;
    letter-spacing: 0.4em;
    text-transform: uppercase;
    border: 2px solid var(--ink);
    padding: 10px 18px;
    margin-bottom: 32px;
  }
  section.closing h1 {
    font-size: 96px;
    line-height: 0.95;
    margin: 0 0 24px 0;
  }
  section.closing .tag {
    font-size: 22px;
    letter-spacing: 0.04em;
    max-width: 900px;
    color: var(--ink);
    border-top: 2px solid var(--ink);
    padding-top: 16px;
  }
---

<!-- _class: title -->
<!-- _paginate: false -->

<div class="chip">Agent Fight Club</div>

<div class="wordmark">Agent<br/><span class="alt">Anatomy</span></div>

<div class="meta">
<span>LOOP · LLM · TOOLS</span>
<span>AGENTFIGHTCLUB.TODAY</span>
</div>

---

<!-- _class: watch big -->

## Agenda

1. Introduction round
2. Part 1: Theory & First steps of agent building
3. Part 2: Build & Compete

---

## Introduction round

<div class="cols3 two">

<div class="card">
<div class="num">// 01</div>
<div class="glyph">🙋</div>
<div class="head">Who are you?</div>
</div>

<div class="card">
<div class="num">// 02</div>
<div class="glyph">🎯</div>
<div class="head">What do you expect from the event and community?</div>
</div>

</div>

---

<!-- _class: equation -->

## What does an agent consist of?

<div class="eqrow">

<div class="eqlead">Agent =</div>

<div class="eqcard">
<div class="glyph">↻</div>
<div class="name">Loop</div>
</div>

<div class="op">+</div>

<div class="eqcard">
<div class="glyph">🧠</div>
<div class="name">LLM</div>
</div>

<div class="op">+</div>

<div class="eqcard">
<div class="glyph">🔌</div>
<div class="name">Environment interaction<span class="sub">(Tools)</span></div>
</div>

</div>

---

<!-- _class: bigtitle -->

<div class="glyph">📐</div>

<div class="num">// Part 1</div>

# Theory<br/>& first steps<br/>of agent building

---

<!-- _class: repo -->

<div class="big">Clone the<br/>repo please</div>

<div class="split">

<div class="qr">
<img src="assets/repo-qr.png" alt="Repository QR code" />
</div>

<div class="urlbox">
<div class="hdr">// git remote</div>
https://github.com/neuromaxer/agent-meetup
</div>

</div>

---

<!-- _class: watch big -->

## Agenda

1. What is an Agent?
2. What is a Harness?
3. What's under the hood of a coding harness?
4. Existing harnesses like **pi**, **OpenCode**

---

<!-- _class: roadmap -->

## Long-term agenda

<div class="grid">

<div class="item now">
<div class="n">01</div>
<div class="t"><span class="stamp">Today</span>Agent Foundations<span class="sub">Agent loop + basic tools</span></div>
</div>

<div class="item">
<div class="n">02</div>
<div class="t">More harness features<span class="sub">Skills, MCP, hooks</span></div>
</div>

<div class="item">
<div class="n">03</div>
<div class="t">Agent memory &amp; search</div>
</div>

<div class="item">
<div class="n">04</div>
<div class="t">Subagents and loops</div>
</div>

<div class="item">
<div class="n">05</div>
<div class="t">Harness internals<span class="sub">Compaction, sandboxes, LLM tokenomics</span></div>
</div>

<div class="item">
<div class="n">06</div>
<div class="t">Agent tooling<span class="sub">Observability, integrations</span></div>
</div>

<div class="item">
<div class="n">07</div>
<div class="t">Self-improving agents<span class="sub">e.g. Hermes, OpenClaw</span></div>
</div>

<div class="item">
<div class="n">08</div>
<div class="t">Dark factories &amp; the future of work</div>
</div>

</div>

---

<!-- _class: llm -->

## LLM basics

<div class="split">

<div>

<div class="lvl l1">
<span class="tag">Machine learning model</span>
<span class="def">Trained on data to predict something.</span>
</div>

<div class="lvl l2">
<span class="tag">Neural network</span>
<span class="def">One way to build that model.</span>
</div>

<div class="lvl l3">
<span class="tag">LLM</span>
<span class="def">A neural network trained on an internet-scale corpus of text — to predict the next word (token).</span>
</div>

</div>

<div>

<div class="termbox">
<div class="hdr">// next-token prediction</div>
"Hello my name <span class="cursor">_</span>"<br/>
→ <span class="out">"is"</span>
</div>

<div class="pipe">
<div class="box">Text in</div>
<div class="arw">→</div>
<div class="box core">LLM</div>
<div class="arw">→</div>
<div class="box">Text out</div>
</div>

<div class="stateless">
<span class="k">⚠ Stateless</span>
No memory between calls. It just continues whatever input you gave it — every single time.
</div>

</div>

</div>

<!--
Speaker: Text in, text out — that's the whole interface (setting multi-modal aside for now).
Statelessness is the key point for what comes next: if the model remembers nothing, then the
loop and the context we hand it are entirely our job. That's what makes an agent an agent.
-->

---

<!-- _class: loop -->

## The agent loop

<div class="diagram">
<img src="assets/agent-loop-diagram.svg" alt="Your prompt → LLM evaluates → tool call(s) → tool result back into the loop; no tool calls → final answer" />
</div>

<div class="beats">
<div class="beat"><span class="k">Loop</span>The model keeps calling tools until it has nothing left to call.</div>
<div class="beat"><span class="k">Exit</span>No tool calls means it's done — that's the final answer.</div>
</div>

<!--
Speaker: This is the whole trick. The model is stateless, so each turn we hand it the prompt
plus everything that happened so far. It either asks for a tool, or it answers. Feeding the
tool result back in is the loop — and that loop is the harness, not the model.
-->

---

<!-- _class: whatis -->

## What is an Agent?

<div class="lead">A software system that can <strong>perceive</strong> information, <strong>reason</strong> about it, and <strong>take actions</strong> to achieve a goal — often with limited human input.</div>

<div class="eq">

<div class="lead-t">Agent =</div>

<div class="card model">
<div class="name">Model</div>
<div class="body">Contains the intelligence.</div>
</div>

<div class="op">+</div>

<div class="card harness">
<div class="name">Harness</div>
<div class="body">Makes that intelligence useful.</div>
</div>

</div>

<div class="rule">If it's not the model, it's the <span class="hl">harness</span></div>

<div class="kicker"><strong>Harness engineering</strong> is how we build systems around models to turn them into work engines.</div>

<!--
Speaker: This is the framing for the whole series. The model is a stateless text predictor —
we just saw that. Everything else, the loop, the tools, the context, the memory, is harness.
That division is why "if it's not the model, it's the harness" is a useful test.
-->

---

<!-- _class: bigtitle -->

<div class="glyph">⚔️</div>

<div class="num">// Part 2</div>

# Build<br/>& compete

---

<!-- _class: bigtitle -->

<div class="glyph">💬</div>

<div class="num">// Wrap</div>

# Feedback<br/>/ Conclusion

---

<!-- _class: divider -->

# Appendix

<div class="rule">Reference material</div>

---

<!-- _class: plate tall -->

## Agent configuration precision trade-off

<div class="frame">
<img src="assets/agent-config-precision.png" alt="Configuration precision required vs model cost / capability" />
</div>

---

<!-- _class: plate wide -->

## AI solution rigidness trade-off

<div class="frame">
<img src="assets/ai-solution-rigidness.png" alt="Spectrum from generic agent to fully programmed workflow" />
</div>

---

<!-- _class: watch big -->

## Game playing agent options

1. Tune your simple agent manually
2. Make coding agent to write game playing agent
3. Use coding agent as your agent (maybe expose later)

---

<!-- _class: watch big -->

## Practical tips

1. Pi as example
2. For safer daily usage use more mainstream harnesses (**Claude Code**, **Codex**, **opencode**)
