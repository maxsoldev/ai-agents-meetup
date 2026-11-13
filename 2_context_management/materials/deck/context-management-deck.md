---
marp: true
paginate: true
size: 16:9
title: Context Management
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
    font-size: 22px;
    letter-spacing: 0.16em;
    text-transform: uppercase;
    color: var(--ink);
    margin: 0 0 18px 0;
    border-bottom: 3px solid var(--ink);
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
  /* two repos: QR on top, URL under it */
  section.repo .pair {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 48px;
    margin-top: 8px;
  }
  section.repo .pair > div { display: flex; flex-direction: column; align-items: center; gap: 18px; }
  section.repo .pair .qr { width: 270px; padding: 14px; }
  section.repo .pair .label {
    font-weight: 700;
    font-size: 22px;
    letter-spacing: 0.14em;
    text-transform: uppercase;
    border-bottom: 2px solid var(--ink);
    padding-bottom: 4px;
  }
  section.repo .pair .urlbox { font-size: 18px; padding: 14px 18px; text-align: center; box-shadow: 6px 6px 0 var(--ink); }

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
  section.loop { justify-content: flex-start; padding-top: 36px; }
  section.loop .beats.three { grid-template-columns: repeat(3, 1fr); margin-top: 26px; }
  section.loop .diagram.dark { background: var(--night); padding: 8px; }
  section.loop .diagram.dark img { width: 92%; }
  section.loop .def {
    border-left: 6px solid var(--ink);
    background: var(--panel);
    padding: 12px 18px;
    font-size: 24px;
    margin-bottom: 16px;
  }
  section.loop .def strong { background: var(--ink); color: var(--bg); padding: 1px 6px; }
  section.loop .def .attrib { display: block; margin-top: 4px; font-size: 13px; letter-spacing: 0.2em; text-transform: uppercase; color: var(--ink-soft); }
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
    grid-template-rows: repeat(4, auto);
    grid-auto-flow: column; /* fill left column top to bottom, then right */
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
  section.roadmap .item.now .t .sub { color: hsla(43, 100%, 90%, 0.82); font-weight: 400; }
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
  section.plate.white .frame { height: 520px; box-sizing: border-box; background: #fff; }
  section.plate.cream .frame { height: 520px; box-sizing: border-box; background: #fcfcfb; }
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
  section.watch.big li { font-size: 24px; padding: 22px 20px 22px 86px; }
  section.watch.big li::before { left: 20px; font-size: 26px; }

  /* ---- Agenda with sub-items: 01 / 1.1 numbering ---- */
  section.agenda ol { counter-reset: a; margin-top: 8px; }
  section.agenda li { list-style: none; counter-increment: a; padding: 8px 0 8px 64px; font-size: 22px; }
  section.agenda > ol > li { font-weight: 700; }
  section.agenda li::before { content: counter(a, decimal-leading-zero); top: 7px; background: var(--ink); color: var(--bg); padding: 0 8px; }
  section.agenda li ol { counter-reset: b; margin-top: 6px; }
  section.agenda li li { counter-increment: b; font-weight: 400; font-size: 19px; padding: 5px 0 5px 52px; }
  section.agenda li li::before { content: counter(a) "." counter(b); top: 5px; background: none; color: var(--ink); padding: 0; }

  /* ---- Sources: course image left, reading list right ---- */
  section.sources .split { display: grid; grid-template-columns: 1.15fr 1fr; gap: 36px; align-items: start; margin-top: 8px; }
  section.sources .frame { border: 3px solid var(--ink); box-shadow: 10px 10px 0 var(--ink); background: var(--night); }
  section.sources .frame img { display: block; width: 100%; }
  section.sources .cap { margin-top: 18px; font-size: 18px; }
  section.sources li { font-size: 18px; padding: 9px 0 9px 28px; }
  section.sources a { color: var(--ink); text-decoration: none; }
  section.sources .url { display: block; font-size: 13px; color: var(--ink-soft); }

  /* ---- Anatomy grid: 8 cards in request order ---- */
  section.anatomy .grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 16px 18px; margin-top: 6px; }
  section.anatomy .c { border: 2px solid var(--ink); background: var(--bg); box-shadow: 5px 5px 0 var(--ink); padding: 10px 14px; }
  section.anatomy .c .h { font-weight: 700; font-size: 18px; letter-spacing: -0.03em; white-space: nowrap; line-height: 1.2; margin-bottom: 6px; }
  section.anatomy .c .h .n { background: var(--ink); color: var(--bg); padding: 0 6px; margin-right: 6px; }
  section.anatomy .c li { font-size: 15px; padding: 4px 0 4px 18px; line-height: 1.3; }
  section.anatomy .c li::before { top: 2px; }
  section.anatomy .c.hidden { border-style: dashed; box-shadow: none; background: var(--panel); }
  section.anatomy .c.out { background: var(--ink); color: var(--bg); }
  section.anatomy .c.out .h, section.anatomy .c.out li::before { color: var(--bg); }
  section.anatomy .c.out .h .n { background: var(--bg); color: var(--ink); }
  section.anatomy .c.out li { border-bottom-color: var(--bg); }

  /* ---- Composition: labelled chart images stacked ---- */
  section.compo .row { display: grid; grid-template-columns: 190px 1fr; gap: 22px; align-items: center; margin-bottom: 14px; }
  section.compo .row .img { width: 92%; }
  section.compo .lbl { font-weight: 700; font-size: 18px; line-height: 1.25; }
  section.compo .lbl span { display: block; font-weight: 400; font-size: 14px; color: var(--ink-soft); }
  section.compo .img { border: 3px solid var(--ink); box-shadow: 7px 7px 0 var(--ink); background: #fff; padding: 6px; }
  section.compo .img.dark { background: #0b0b0b; }
  section.compo .img img { display: block; width: 100%; }
  section.compo .take, section.tokenomics .take { border: 3px solid var(--ink); background: var(--paper); box-shadow: 7px 7px 0 var(--hot); padding: 10px 18px; font-weight: 700; font-size: 21px; text-align: center; margin-top: 6px; }
  section.compo .take .hl, section.tokenomics .take .hl { background: var(--ink); color: var(--bg); padding: 0 6px; }

  /* ---- Tokenomics: one stacked bar + per-stage bars ---- */
  section.tokenomics .k { font-size: 13px; letter-spacing: 0.2em; text-transform: uppercase; font-weight: 700; margin: 6px 0 8px; }
  section.tokenomics .stack { display: flex; height: 58px; border: 3px solid var(--ink); box-shadow: 6px 6px 0 var(--ink); }
  section.tokenomics .stack div { display: flex; flex-direction: column; justify-content: center; padding: 0 14px; font-size: 14px; line-height: 1.15; border-right: 3px solid var(--ink); }
  section.tokenomics .stack div:last-child { border-right: none; }
  section.tokenomics .stack b { font-size: 20px; }
  section.tokenomics .stack .in { background: var(--ink); color: var(--bg); }
  section.tokenomics .stack .rs { background: var(--hot); color: #fff; }
  section.tokenomics .stack .ou { background: var(--paper); }
  section.tokenomics .bars { margin-top: 4px; }
  section.tokenomics .bar { display: grid; grid-template-columns: 250px 1fr; gap: 14px; align-items: center; font-size: 16px; margin-bottom: 7px; }
  section.tokenomics .bar .fill { height: 26px; background: var(--ink); color: var(--bg); font-weight: 700; font-size: 15px; display: flex; align-items: center; padding-left: 8px; white-space: nowrap; }
  section.tokenomics .bar .fill.hot { background: var(--hot); color: #fff; }
  section.tokenomics .bar .fill.lo { background: transparent; color: var(--ink); border-left: 6px solid var(--ink); }
  section.tokenomics .bar .note { font-size: 13px; color: var(--ink-soft); }
  section.tokenomics .bar .track { display: flex; align-items: center; gap: 10px; }
  section.tokenomics .bar .fill { justify-self: start; }
  section.tokenomics .w1 { width: 99%; } section.tokenomics .w2 { width: 44.7%; } section.tokenomics .w3 { width: 33.5%; }
  section.tokenomics .w4 { width: 17.2%; } section.tokenomics .w5 { width: 14.3%; } section.tokenomics .w6 { width: 4%; }
  section.tokenomics .stack .in { flex: 53.9; } section.tokenomics .stack .rs { flex: 21.6; } section.tokenomics .stack .ou { flex: 24.4; }
  section.tokenomics .k.gap { margin-top: 26px; }
  section.tokenomics .take { margin-top: 14px; }
  section.tokenomics .src { margin-top: 10px; font-size: 13px; color: var(--ink-soft); }
  section.tokenomics .src a { color: var(--ink); }

  /* ---- Pull line: smaller sub-line under the main statement ---- */
  section.pull .line.rot { font-size: 64px; line-height: 1.22; }
  section.compo .take .small { font-size: 16px; font-weight: 400; }
  section.compo .take .tip { font-weight: 700; letter-spacing: 0.15em; margin-right: 6px; }
  section.pull .sub { margin-top: 28px; font-size: 26px; border-top: 2px solid var(--ink); padding-top: 14px; max-width: 1080px; }
  section.pull .sub strong { background: var(--ink); color: var(--bg); padding: 0 6px; }

  /* ---- Context rot: reasons, costs, causes, numbers ---- */
  section.rot .cols3 .card ul { margin-top: 2px; }
  section.rot .cols3 .card li { font-size: 17px; padding: 6px 0 6px 24px; }
  section.rot .take { border: 3px solid var(--ink); background: var(--paper); box-shadow: 7px 7px 0 var(--hot); padding: 10px 18px; font-weight: 700; font-size: 21px; text-align: center; margin-top: 26px; }
  section.rot .take .hl { background: var(--ink); color: var(--bg); padding: 0 6px; }
  section.plate .take { border: 3px solid var(--ink); background: var(--paper); box-shadow: 7px 7px 0 var(--hot); padding: 10px 18px; font-weight: 700; font-size: 19px; text-align: center; margin-top: 24px; }
  section.plate .frame.short { height: 475px; padding: 8px 12px; }
  section.plate .caption { margin-top: 26px; font-size: 20px; text-align: center; color: var(--ink); }
  section.plate .take .hl { background: var(--ink); color: var(--bg); padding: 0 6px; }
  section.rot .src { margin-top: 20px; font-size: 13px; color: var(--ink-soft); }
  section.rot .grp { display: grid; grid-template-columns: repeat(4, 1fr); gap: 0 18px; }
  section.rot .grp .g { grid-column: span 2; font-size: 13px; font-weight: 700; letter-spacing: 0.2em; text-transform: uppercase; border-bottom: 3px solid var(--ink); padding-bottom: 4px; margin-bottom: 12px; }
  section.rot .grp .cost { border: 2px solid var(--ink); box-shadow: 5px 5px 0 var(--ink); padding: 12px 14px; }
  section.rot .grp .cost.q { background: var(--ink); color: var(--bg); }
  section.rot .cost .n { font-size: 13px; letter-spacing: 0.2em; }
  section.rot .cost .t { font-weight: 700; font-size: 22px; text-transform: uppercase; letter-spacing: -0.02em; margin: 2px 0 6px; }
  section.rot .cost .d { font-size: 15px; line-height: 1.35; }
  section.rot .bad { margin-top: 26px; border: 2px dashed var(--ink); background: var(--panel); padding: 12px 16px; }
  section.rot .bad .k { font-size: 13px; font-weight: 700; letter-spacing: 0.2em; text-transform: uppercase; margin-bottom: 10px; }
  section.rot .bad .chips { display: grid; grid-template-columns: repeat(4, 1fr); gap: 14px; }
  section.rot .bad .chips div { font-size: 14px; line-height: 1.3; }
  section.rot .bad .chips b { display: block; font-size: 17px; }
  section.rot .tiles { display: grid; grid-template-columns: 170px repeat(3, 1fr); gap: 14px 16px; align-items: stretch; }
  section.rot .tiles .rl { font-weight: 700; font-size: 16px; line-height: 1.25; align-self: center; }
  section.rot .tiles .rl span { display: block; font-weight: 400; font-size: 12px; color: var(--ink-soft); margin-top: 4px; }
  section.rot .tile { border: 2px solid var(--ink); box-shadow: 5px 5px 0 var(--ink); background: var(--bg); padding: 10px 14px; }
  section.rot .tile.dark { background: var(--ink); color: var(--bg); }
  section.rot .tile .big { font-weight: 700; font-size: 34px; letter-spacing: -0.04em; line-height: 1.05; }
  section.rot .tile .d { font-size: 14px; line-height: 1.3; margin-top: 4px; }
  section.rot .tile .s { font-size: 11px; letter-spacing: 0.12em; text-transform: uppercase; margin-top: 6px; opacity: 0.7; }

  /* ---- Caching: quote + what/how, benefits tiles ---- */
  section.cache .q { border-left: 8px solid var(--ink); background: var(--panel); padding: 14px 20px; font-size: 24px; font-weight: 700; line-height: 1.3; }
  section.cache .q .hl { background: var(--ink); color: var(--bg); padding: 0 6px; }
  section.cache .q .attrib { display: block; margin-top: 6px; font-size: 13px; font-weight: 400; letter-spacing: 0.2em; text-transform: uppercase; color: var(--ink-soft); }
  section.cache .two { display: grid; grid-template-columns: 1fr 1.25fr; gap: 24px; margin-top: 22px; }
  section.cache .two + .q { margin-top: 28px; }
  section.cache .box { border: 2px solid var(--ink); box-shadow: 6px 6px 0 var(--ink); background: var(--bg); padding: 14px 18px; }
  section.cache .box .k { font-size: 13px; font-weight: 700; letter-spacing: 0.2em; text-transform: uppercase; margin-bottom: 8px; }
  section.cache .box p { font-size: 18px; line-height: 1.4; margin: 0 0 8px; }
  section.cache .box p strong { background: var(--ink); color: var(--bg); padding: 0 5px; }
  section.cache .flow { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-top: 4px; }
  section.cache .flow .step { grid-column: span 2; border: 2px solid var(--ink); padding: 8px 12px; font-size: 16px; text-align: center; font-weight: 700; }
  section.cache .flow .hit { background: var(--ink); color: var(--bg); border: 2px solid var(--ink); padding: 8px 12px; font-size: 15px; }
  section.cache .flow .miss { background: var(--hot); color: #fff; border: 2px solid var(--ink); padding: 8px 12px; font-size: 15px; }
  section.cache .flow b { display: block; font-size: 17px; }
  section.cache .ben { display: grid; grid-template-columns: repeat(4, 1fr); gap: 16px; margin-top: 8px; }
  section.cache .ben .t { border: 2px solid var(--ink); box-shadow: 5px 5px 0 var(--ink); background: var(--bg); padding: 12px 14px; display: flex; flex-direction: column; gap: 6px; }
  section.cache .ben .t.dark { background: var(--ink); color: var(--bg); }
  section.cache .ben .big { font-weight: 700; font-size: 40px; letter-spacing: -0.04em; line-height: 1; }
  section.cache .ben .h { font-weight: 700; font-size: 17px; text-transform: uppercase; }
  section.cache .ben .d { font-size: 14px; line-height: 1.35; }
  section.cache .ben .s { font-size: 11px; letter-spacing: 0.12em; text-transform: uppercase; opacity: 0.7; margin-top: auto; }
  section.cache .take { border: 3px solid var(--ink); background: var(--paper); box-shadow: 7px 7px 0 var(--hot); padding: 10px 18px; font-weight: 700; font-size: 20px; text-align: center; margin-top: 24px; }
  section.cache .take .hl { background: var(--ink); color: var(--bg); padding: 0 6px; }
  section.cache .src { margin-top: 14px; font-size: 13px; color: var(--ink-soft); }
  section.plate.short .frame { height: 400px; box-sizing: border-box; background: #fff; padding: 10px 14px; }
  section.plate.miss .frame { height: 470px; box-sizing: border-box; background: #fcfcfb; padding: 10px; }
  section.plate.trap .frame { height: 420px; box-sizing: border-box; background: #212121; padding: 14px; }
  section.plate.pce .frame { height: 540px; box-sizing: border-box; background: #f0eee8; padding: 10px; }
  section.plate .note.src { box-shadow: none; border: none; background: none; text-align: left; font-size: 13px; color: var(--ink-soft); padding: 0; margin-top: 18px; }

  section.cache .ben.three { grid-template-columns: repeat(3, 1fr); gap: 20px; }
  section.cache .ben .big.sm { font-size: 30px; }
  section.cache .ben li { font-size: 15px; padding: 4px 0 4px 20px; line-height: 1.3; }
  section.cache .ben li::before { top: 3px; }
  section.cache .ben .t.dark li { border-bottom-color: var(--bg); }
  section.cache .ben .t.dark li::before { color: var(--bg); }
  section.cache .ben .t.hot { background: var(--hot); color: #fff; }
  section.cache .ben .t.hot li { border-bottom-color: #fff; }
  section.cache .ben .t.hot li::before { color: #fff; }
  section.cache .ben .tag { font-size: 12px; letter-spacing: 0.14em; text-transform: uppercase; border-top: 1px solid currentColor; padding-top: 6px; margin-top: auto; }

  /* ---- Context engineering: definition, four moves, family slides ---- */
  section.ce .hl { background: var(--ink); color: var(--bg); padding: 0 6px; }
  section.ce .dark .hl { background: var(--bg); color: var(--ink); }
  section.ce .def { font-weight: 700; font-size: 30px; line-height: 1.4; letter-spacing: -0.03em; margin: 4px 0 22px; }
  section.ce .def strong { background: var(--ink); color: var(--bg); padding: 0 6px; }
  section.ce .quotes { display: grid; grid-template-columns: repeat(3, 1fr); gap: 18px; }
  section.ce .qc { border: 2px solid var(--ink); box-shadow: 6px 6px 0 var(--ink); background: var(--bg); padding: 14px 16px; font-size: 18px; line-height: 1.38; font-weight: 700; display: flex; flex-direction: column; }
  section.ce .qc.dark { background: var(--ink); color: var(--bg); }
  section.ce .dark code { color: var(--bg); border-color: var(--bg); background: hsla(43, 100%, 50%, 0.12); }
  section.ce code { white-space: nowrap; }
  section.ce .qc .attrib { margin-top: auto; padding-top: 10px; font-size: 12px; font-weight: 400; letter-spacing: 0.2em; text-transform: uppercase; opacity: 0.75; }
  section.ce .vs { display: grid; grid-template-columns: 1fr 50px 1.3fr; align-items: stretch; margin-top: 30px; }
  section.ce .vs > div { border: 2px solid var(--ink); padding: 10px 16px; font-size: 17px; line-height: 1.35; }
  section.ce .vs > div.arrow { border: none; display: flex; align-items: center; justify-content: center; font-size: 30px; font-weight: 700; }
  section.ce .vs > div.on { background: var(--ink); color: var(--bg); box-shadow: 6px 6px 0 var(--hot); }
  section.ce .vs b { display: block; font-size: 15px; letter-spacing: 0.16em; text-transform: uppercase; margin-bottom: 2px; }

  section.ce .moves { display: grid; grid-template-columns: repeat(4, 1fr); gap: 16px; margin-top: 4px; }
  section.ce .m { border: 2px solid var(--ink); box-shadow: 6px 6px 0 var(--ink); background: var(--bg); padding: 12px 14px; display: flex; flex-direction: column; gap: 6px; }
  section.ce .m.dark { background: var(--ink); color: var(--bg); }
  section.ce .m .n { font-size: 12px; letter-spacing: 0.24em; }
  section.ce .m .v { font-weight: 700; font-size: 30px; text-transform: uppercase; letter-spacing: -0.04em; line-height: 1; }
  section.ce .m .d { font-size: 15px; font-weight: 700; line-height: 1.3; min-height: 40px; }
  section.ce .m li { font-size: 14px; padding: 4px 0 4px 18px; line-height: 1.3; }
  section.ce .m li::before { top: 3px; }
  section.ce .m.dark li { border-bottom-color: var(--bg); }
  section.ce .m.dark li::before { color: var(--bg); }
  section.ce .m .loss { margin-top: auto; border-top: 2px solid currentColor; padding-top: 6px; font-size: 13px; line-height: 1.3; }
  section.ce .m .loss b { color: var(--hot); text-transform: uppercase; letter-spacing: 0.12em; font-size: 12px; }
  section.ce .m.dark .loss b { color: var(--bg); }
  section.ce .bar { margin-top: 22px; border: 3px solid var(--ink); background: var(--hot); color: #fff; padding: 8px 16px; font-size: 18px; font-weight: 700; }
  section.ce .bar b { letter-spacing: 0.16em; text-transform: uppercase; font-size: 14px; margin-right: 12px; }

  section.ce .lv { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-top: 2px; }
  section.ce .lv.three { grid-template-columns: repeat(3, 1fr); gap: 16px; }
  section.ce .col { border: 2px solid var(--ink); box-shadow: 5px 5px 0 var(--ink); background: var(--bg); padding: 10px 14px; }
  section.ce .col.dark { background: var(--ink); color: var(--bg); }
  section.ce .col .k { font-weight: 700; font-size: 18px; text-transform: uppercase; letter-spacing: -0.01em; }
  section.ce .col .k span { display: block; font-size: 12px; font-weight: 400; letter-spacing: 0.18em; opacity: 0.75; margin-top: 2px; }
  section.ce .col .p { font-size: 13px; line-height: 1.3; font-style: italic; opacity: 0.8; margin: 4px 0 2px; }
  section.ce .col li { font-size: 14px; padding: 5px 0 5px 18px; line-height: 1.3; }
  section.ce .col li::before { top: 4px; }
  section.ce .col.dark li { border-bottom-color: var(--bg); }
  section.ce .col.dark li::before, section.ce .col.dark strong { color: var(--bg); }

  section.ce .costs { margin-top: 18px; border: 2px dashed var(--ink); background: var(--panel); padding: 8px 14px; }
  section.ce .costs .k { font-size: 12px; font-weight: 700; letter-spacing: 0.2em; text-transform: uppercase; margin-bottom: 6px; }
  section.ce .costs .chips { display: grid; grid-template-columns: repeat(4, 1fr); gap: 14px; }
  section.ce .costs .chips div { font-size: 13px; line-height: 1.3; }
  section.ce .costs .chips b { display: block; font-size: 15px; }

  section.ce .take { border: 3px solid var(--ink); background: var(--paper); box-shadow: 7px 7px 0 var(--hot); padding: 8px 18px; font-weight: 700; font-size: 20px; text-align: center; margin-top: 18px; }
  section.ce .src { margin-top: 10px; font-size: 12px; color: var(--ink-soft); }

  section.ce .axes { display: grid; grid-template-columns: 170px 1fr 1fr; gap: 8px; }
  section.ce .axes > div { border: 2px solid var(--ink); padding: 8px 12px; font-size: 15px; line-height: 1.3; }
  section.ce .axes .h { border: none; font-size: 12px; font-weight: 700; letter-spacing: 0.18em; text-transform: uppercase; align-self: end; padding-bottom: 2px; }
  section.ce .axes .r { border: none; font-weight: 700; font-size: 15px; align-self: center; }
  section.ce .axes .r span { display: block; font-weight: 400; font-size: 12px; color: var(--ink-soft); }
  section.ce .axes .cc { background: var(--ink); color: var(--bg); }
  section.ce .axes b { display: block; font-size: 16px; }
  section.ce .chain { display: grid; grid-template-columns: 110px 1fr 30px 1fr 30px 1fr; gap: 8px 6px; align-items: center; margin-top: 8px; font-size: 14px; }
  section.ce .chain .lbl { font-weight: 700; font-size: 14px; text-transform: uppercase; }
  section.ce .chain .s { border: 2px solid var(--ink); padding: 5px 10px; background: var(--bg); line-height: 1.25; }
  section.ce .chain .s.first { background: var(--ink); color: var(--bg); }
  section.ce .chain .a { text-align: center; font-weight: 700; }
  /* big variants: bigger tiles, both blocks on one slide */
  section.ce .axes.big { grid-template-columns: 190px 1fr 1fr; gap: 12px 16px; }
  section.ce .axes.big > div:not(.h):not(.r) { padding: 14px 18px; min-height: 86px; box-shadow: 5px 5px 0 var(--ink); background: var(--bg); font-size: 18px; line-height: 1.35; display: flex; flex-direction: column; justify-content: center; }
  section.ce .axes.big > div.cc:not(.h):not(.r) { background: var(--ink); box-shadow: 5px 5px 0 var(--hot); }
  section.ce .axes.big b { font-size: 23px; letter-spacing: -0.02em; margin-bottom: 4px; }
  section.ce .axes.big .h { font-size: 13px; }
  section.ce .axes.big .r { font-size: 22px; }
  section.ce .axes.big .r span { font-size: 13px; letter-spacing: 0.16em; text-transform: uppercase; }
  section.ce .chain.big { grid-template-columns: 110px 1fr 28px 1.15fr 28px 1.15fr; gap: 12px 6px; margin-top: 10px; font-size: 16px; }
  section.ce .chain.big .lbl { font-size: 16px; }
  section.ce .chain.big .s { padding: 10px 14px; box-shadow: 4px 4px 0 var(--ink); }
  section.ce .chain.big .s.first { box-shadow: 4px 4px 0 var(--hot); }
  section.ce .chain.big .a { font-size: 22px; }
  section.ce .lv.gap { margin-top: 24px; }
  section.ce .sub.top { margin-top: 0; }
  section.ce .sub { font-size: 12px; font-weight: 700; letter-spacing: 0.2em; text-transform: uppercase; margin: 18px 0 4px; }

  section.ce .tiles { display: grid; grid-template-columns: repeat(4, 1fr); gap: 14px; }
  section.ce .tiles.three { grid-template-columns: repeat(3, 1fr); }
  section.ce .tile { border: 2px solid var(--ink); box-shadow: 5px 5px 0 var(--ink); background: var(--bg); padding: 8px 12px; }
  section.ce .tile.dark { background: var(--ink); color: var(--bg); }
  section.ce .tile.hot { background: var(--hot); color: #fff; }
  section.ce .tile .big { font-weight: 700; font-size: 30px; letter-spacing: -0.04em; line-height: 1.05; }
  section.ce .tile .d { font-size: 13px; line-height: 1.3; margin-top: 4px; }
  section.ce .tile .s { font-size: 10px; letter-spacing: 0.12em; text-transform: uppercase; margin-top: 4px; opacity: 0.7; }
  /* move summary bar: first slide of each move */
  section.ce .movehead { display: flex; align-items: baseline; gap: 18px; background: var(--ink); color: var(--bg); box-shadow: 6px 6px 0 var(--hot); padding: 10px 20px; margin-bottom: 20px; }
  section.ce .movehead .n { font-size: 13px; letter-spacing: 0.24em; }
  section.ce .movehead .v { font-weight: 700; font-size: 30px; text-transform: uppercase; letter-spacing: -0.04em; }
  section.ce .movehead .d { font-weight: 700; font-size: 20px; }
  section.ce .q { border-left: 8px solid var(--ink); background: var(--panel); padding: 8px 16px; font-size: 20px; font-weight: 700; margin-bottom: 14px; }
  section.ce .q .attrib { display: block; margin-top: 4px; font-size: 12px; font-weight: 400; letter-spacing: 0.2em; text-transform: uppercase; color: var(--ink-soft); }
  section.ce .knobs { display: grid; grid-template-columns: 150px repeat(3, 1fr); gap: 12px; margin-top: 16px; align-items: stretch; }
  section.ce .knobs .lbl { font-weight: 700; font-size: 14px; text-transform: uppercase; align-self: center; }
  section.ce .knobs > div:not(.lbl) { border: 2px dashed var(--ink); background: var(--panel); padding: 6px 12px; font-size: 13px; line-height: 1.3; }
  section.ce .knobs b { display: block; font-size: 15px; }

  section.ce table { width: 100%; border-collapse: collapse; font-size: 15px; margin-top: 4px; }
  section.ce th { background: var(--ink); color: var(--bg); text-align: left; padding: 6px 10px; font-size: 13px; letter-spacing: 0.14em; text-transform: uppercase; }
  section.ce td { border-bottom: 1px dashed var(--ink); padding: 6px 10px; background: transparent; line-height: 1.3; }
  section.ce td:first-child { font-weight: 700; white-space: nowrap; }
  section.ce tr { background: transparent !important; }


  /* ---- Takeaways: one line + numbered claim → action rows ---- */
  section.tk .one { background: var(--ink); color: var(--bg); padding: 12px 18px; font-size: 21px; font-weight: 700; line-height: 1.3; box-shadow: 7px 7px 0 var(--hot); margin-bottom: 18px; }
  section.tk .one .k { display: block; font-size: 12px; font-weight: 400; letter-spacing: 0.2em; text-transform: uppercase; opacity: 0.75; margin-bottom: 2px; }
  section.tk .rows { display: grid; grid-template-columns: 44px 1.25fr 1fr; gap: 0; border: 2px solid var(--ink); }
  section.tk .rows > div { padding: 9px 12px; border-bottom: 1px dashed var(--ink); font-size: 16px; line-height: 1.3; }
  section.tk .rows > div:nth-last-child(-n+3) { border-bottom: none; }
  section.tk .rows .n { background: var(--ink); color: var(--bg); font-weight: 700; text-align: center; border-bottom-color: var(--bg); }
  section.tk .rows .c { font-weight: 700; }
  section.tk .rows .a { background: var(--paper); }

  /* ---- v2: context engineering, spread out ---- */
  /* demo / voice-over banner: frames the live example */
  section.ce .demo { display: flex; gap: 14px; align-items: center; background: var(--night); color: var(--night-fg); border: 2px solid var(--ink); box-shadow: 5px 5px 0 var(--hot); padding: 9px 16px; font-size: 17px; line-height: 1.35; margin-top: 20px; }
  section.ce .demo .tag { flex: none; background: var(--hot); color: #fff; font-weight: 700; letter-spacing: 0.2em; font-size: 12px; padding: 3px 8px; text-transform: uppercase; }
  section.ce .demo.extra .tag { background: var(--bg); color: var(--ink); }
  section.ce .demo.voice .tag { background: transparent; color: var(--night-fg); border: 1px solid var(--night-fg); }
  section.ce .demo b { color: #fff; }
  section.ce .demo code { color: var(--night-fg); border-color: var(--night-fg); background: transparent; }
  /* ask the room */
  section.ce .ask { border: 3px dashed var(--hot); background: var(--paper); padding: 8px 16px; font-size: 18px; font-weight: 700; margin-top: 16px; }
  section.ce .ask .k { color: var(--hot); font-size: 12px; letter-spacing: 0.22em; margin-right: 10px; }
  /* in your daily work */
  section.ce .daily { margin-top: 20px; border: 3px solid var(--ink); background: var(--paper); box-shadow: 7px 7px 0 var(--hot); padding: 12px 18px; }
  section.ce .daily .k { font-size: 13px; font-weight: 700; letter-spacing: 0.2em; text-transform: uppercase; margin-bottom: 4px; }
  section.ce .daily li { font-size: 19px; padding: 6px 0 6px 26px; font-weight: 700; }
  section.ce .daily li::before { top: 5px; }
  /* bigger columns for spread-out slides */
  section.ce .col.big { padding: 16px 20px; }
  section.ce .col.big .k { font-size: 22px; }
  section.ce .col.big .k span { font-size: 13px; }
  section.ce .col.big .p { font-size: 16px; }
  section.ce .col.big li { font-size: 18px; padding: 8px 0 8px 22px; }
  section.ce .col.big li::before { top: 7px; }
  section.ce .problem { border-left: 8px solid var(--hot); background: var(--panel); padding: 10px 18px; font-size: 21px; font-weight: 700; margin-bottom: 20px; }
  section.ce .problem .k { display: block; font-size: 12px; letter-spacing: 0.22em; text-transform: uppercase; color: var(--hot); margin-bottom: 2px; }
  /* three paths for big output */
  section.ce .paths { display: grid; grid-template-columns: repeat(3, 1fr); gap: 18px; }
  section.ce .path { border: 2px solid var(--ink); box-shadow: 6px 6px 0 var(--ink); background: var(--bg); padding: 12px 16px; display: flex; flex-direction: column; gap: 8px; }
  section.ce .path.bad { background: var(--ink); color: var(--bg); box-shadow: 6px 6px 0 var(--hot); }
  section.ce .path .n { font-size: 12px; letter-spacing: 0.24em; }
  section.ce .path .h { font-weight: 700; font-size: 22px; text-transform: uppercase; letter-spacing: -0.02em; }
  section.ce .path pre { margin: 0; font-size: 13px; padding: 8px 10px; box-shadow: none; white-space: pre-wrap; }
  section.ce .path.bad pre { border-color: var(--bg); }
  section.ce .path .in { margin-top: auto; border-top: 2px solid currentColor; padding-top: 8px; font-size: 16px; line-height: 1.3; }
  section.ce .path .in b { display: block; font-size: 24px; letter-spacing: -0.03em; }
  section.ce .note { margin-top: 18px; font-size: 17px; line-height: 1.4; border-left: 6px solid var(--ink); background: var(--panel); padding: 8px 14px; }
  /* flow of steps */
  section.ce .flow { display: grid; grid-auto-flow: column; grid-auto-columns: 1fr; gap: 0; align-items: stretch; }
  section.ce .flow .st { border: 2px solid var(--ink); background: var(--bg); padding: 10px 12px; font-size: 16px; line-height: 1.3; position: relative; margin-right: 22px; box-shadow: 4px 4px 0 var(--ink); }
  section.ce .flow .st:last-child { margin-right: 0; }
  section.ce .flow .st::after { content: '→'; position: absolute; right: -21px; top: 40%; font-weight: 700; font-size: 18px; }
  section.ce .flow .st:last-child::after { content: none; }
  section.ce .flow .st.dark { background: var(--ink); color: var(--bg); }
  section.ce .flow .st.hot { background: var(--hot); color: #fff; }
  section.ce .flow .st b { display: block; font-size: 12px; letter-spacing: 0.18em; text-transform: uppercase; margin-bottom: 4px; }
  section.ce .flow .st code { white-space: normal; }
  section.ce .flow .st.dark code, section.ce .flow .st.hot code { color: inherit; border-color: currentColor; background: transparent; }
  /* setting slide */
  section.ce .setting { display: grid; grid-template-columns: 1fr 1fr; gap: 24px; }
  section.ce .panels .p { display: grid; grid-template-columns: 120px 1fr; gap: 12px; padding: 8px 0; border-bottom: 1px dashed var(--ink); font-size: 17px; line-height: 1.3; }
  section.ce .panels .p:last-child { border-bottom: none; }
  section.ce .panels .p b { background: var(--ink); color: var(--bg); padding: 2px 8px; text-align: center; align-self: start; font-size: 15px; }
  section.ce .scenes { display: grid; grid-template-columns: repeat(4, 1fr); gap: 14px; margin-top: 22px; }
  section.ce .scene { border: 2px solid var(--ink); box-shadow: 5px 5px 0 var(--ink); background: var(--bg); padding: 10px 14px; }
  section.ce .scene .v { font-weight: 700; font-size: 20px; text-transform: uppercase; letter-spacing: -0.03em; }
  section.ce .scene .d { font-size: 15px; line-height: 1.3; margin-top: 4px; }
  /* before/after context stacks */
  section.ce .ba { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 18px; }
  section.ce .ba .colh { font-weight: 700; font-size: 18px; text-transform: uppercase; margin-bottom: 8px; }
  section.ce .ba .colh span { display: block; font-size: 12px; font-weight: 400; letter-spacing: 0.16em; opacity: 0.75; }
  section.ce .ba .it { border: 2px solid var(--ink); padding: 4px 10px; font-size: 14px; line-height: 1.25; margin-bottom: 5px; background: var(--bg); }
  section.ce .ba .it.sys { background: var(--panel-strong); }
  section.ce .ba .it.tool { background: var(--ink); color: var(--bg); }
  section.ce .ba .it.cleared { background: var(--paper); border-style: dashed; color: var(--ink-soft); }
  section.ce .ba .it.sum { background: var(--hot); color: #fff; font-weight: 700; }
  section.ce .ba .cost { margin-top: 8px; font-size: 14px; line-height: 1.35; border-top: 2px solid var(--ink); padding-top: 6px; }
  section.ce .ba .cost b { color: var(--hot); }
  /* quiz */
  section.ce .quiz { display: grid; grid-template-columns: repeat(4, 1fr); gap: 16px; margin-top: 8px; }
  section.ce .quiz .qi { border: 2px solid var(--ink); box-shadow: 5px 5px 0 var(--ink); background: var(--bg); padding: 14px 14px; min-height: 120px; display: flex; flex-direction: column; justify-content: space-between; }
  section.ce .quiz .qi .f { font-weight: 700; font-size: 19px; line-height: 1.3; }
  section.ce .quiz .qi .f span { display: block; font-weight: 400; font-size: 14px; color: var(--ink-soft); margin-top: 4px; }
  section.ce .quiz .qi .a { margin-top: 10px; font-weight: 700; font-size: 15px; letter-spacing: 0.14em; text-transform: uppercase; background: var(--ink); color: var(--bg); padding: 3px 8px; align-self: flex-start; }
  section.ce .quiz .qi .a.q { background: transparent; color: var(--ink-faint); border: 2px dashed var(--ink-faint); }
  section.ce pre code { white-space: pre; font-size: 15px; }
  section.ce .path pre code { font-size: 13px; }
  section.ce .flow .st::after { color: var(--ink); }
  section.ce .cmp { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
  section.ce .cmp .big { font-weight: 700; font-size: 28px; letter-spacing: -0.03em; }

  section.ce .costs { padding: 14px 18px; }
  section.ce .costs .chips div { font-size: 16px; line-height: 1.35; }
  section.ce .costs .chips b { font-size: 19px; margin-bottom: 4px; }
  section.ce .axes.big.three { grid-template-columns: 150px 1fr 1fr 1fr; }

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
    width: fit-content; margin-left: auto; margin-right: auto;
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
    margin-left: auto; margin-right: auto;
  }
---

<!-- _class: title -->
<!-- _paginate: false -->

<div class="chip">Agent Fight Club #4</div>

<div class="wordmark">Context<br/><span class="alt">Management</span></div>

<div class="meta">
<span>ANATOMY · ROT · CACHING · TECHNIQUES</span>
<span>AGENTFIGHTCLUB.TODAY</span>
</div>

---

<!-- _class: repo -->

<div class="big">Clone the repos please</div>

<div class="pair">

<div>
<div class="label">Deck &amp; Notes</div>
<div class="qr"><img src="../images/qr-agent-meetup.png" alt="agent-meetup QR code" /></div>
<div class="urlbox">https://github.com/maxsoldev/agent-meetup</div>
</div>

<div>
<div class="label">Eduagent Harness</div>
<div class="qr"><img src="../images/qr-eduagent.png" alt="eduagent QR code" /></div>
<div class="urlbox">https://github.com/maxsoldev/eduagent</div>
</div>

</div>

---

<!-- _class: watch big -->

## Agenda

1. Introduction round
2. Part 1: Theory of context management
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

<!-- _class: roadmap -->

## Long-term agenda

<div class="grid">

<div class="item">
<div class="n">01</div>
<div class="t">Agent Foundations<span class="sub">Agent loop + basic tools</span></div>
</div>

<div class="item now">
<div class="n">02</div>
<div class="t"><span class="stamp">Today</span>Context Management<span class="sub">Anatomy, context rot, caching, compaction</span></div>
</div>

<div class="item">
<div class="n">03</div>
<div class="t">More harness features<span class="sub">Skills, MCP, hooks</span></div>
</div>

<div class="item">
<div class="n">04</div>
<div class="t">Agent memory &amp; search<span class="sub">RAG, web search</span></div>
</div>

<div class="item">
<div class="n">05</div>
<div class="t">Self-improving agents<span class="sub">e.g. Hermes, OpenClaw</span></div>
</div>

<div class="item">
<div class="n">06</div>
<div class="t">Agent-to-Agent (A2A)<span class="sub">Agentic commerce</span></div>
</div>

<div class="item">
<div class="n">07</div>
<div class="t">AgentOps<span class="sub">Observability, evals</span></div>
</div>

<div class="item">
<div class="n">08</div>
<div class="t">Dark factories &amp; the future of work</div>
</div>

</div>

---

<!-- _class: bigtitle -->

<div class="num">Part 1</div>

# Context Management

<div class="kicker">"A lot of apparent <strong>“model quality”</strong> is really context quality"<br/>— Sebastian Raschka</div>

---

<!-- _class: agenda -->

## Agenda for today

1. Context Management Overview
   1. Context Anatomy: what is in the context window. Demo: eduagent
   2. Context Rot: why longer context hurts
   3. Caching: make-it-or-break-it for prod agents
   4. Context engineering: four strategies, live on a real repo
   5. Takeaways for your daily work with agents
2. Workshop: manage context for trader agents

---

<!-- _class: sources -->

## Suggested sources

<div class="split">

<div>
<div class="frame"><img src="../images/cmu-agents-course.png" /></div>
<div class="cap"><strong>CMU 11-768 AI Agents 2026</strong> · Neubig &amp; Fried<br/><a href="https://www.youtube.com/playlist?list=PLSN0qpDfUvTM"><span class="url">youtube.com/playlist?list=PLSN0qpDfUvTM</span></a></div>
</div>

<div>

- <a href="https://code.claude.com/docs/en/how-claude-code-works"><strong>How Claude Code works</strong><span class="url">code.claude.com/docs/en/how-claude-code-works</span></a>
- <a href="https://manus.im/blog/Context-Engineering-for-AI-Agents-Lessons-from-Building-Manus"><strong>Manus: Context Engineering for AI Agents</strong><span class="url">manus.im/blog</span></a>
- <a href="https://magazine.sebastianraschka.com/p/components-of-a-coding-agent"><strong>Raschka: Components of a Coding Agent</strong><span class="url">magazine.sebastianraschka.com</span></a>
- <a href="https://blog.langchain.com/context-engineering-for-agents/"><strong>LangChain: Context Engineering for Agents</strong><span class="url">blog.langchain.com/context-engineering-for-agents</span></a>

</div>

</div>

---

<!-- _class: bigtitle -->

<div class="num">1.1</div>

# Context Anatomy

<div class="kicker">What the model actually receives. Spoiler: <strong>far more</strong> than your prompts and tool results.</div>

---

<!-- _class: loop -->

## Agent loop refresher

<div class="def">An agent is <strong>an LLM autonomously using tools in a loop</strong><span class="attrib">— Simon Willison</span></div>

<div class="diagram"><img src="../images/agent-loop-diagram-afc.svg" alt="Your prompt → LLM evaluates → execute tools → tool result back into the loop; no tool calls → final answer" /></div>

<div class="beats three">
<div class="beat"><span class="k">Agent turn</span>One pass through the loop: one model call plus the tool calls it asks for.</div>
<div class="beat"><span class="k">Agent run</span>One user message and all the turns after it, until the model replies with no tool calls.</div>
<div class="beat"><span class="k">Agent session</span>All the runs that share one message history.</div>
</div>

---

<!-- _class: plate cream -->

## Context window

<div class="frame short"><img src="../images/context-window-cropped.png" /></div>

<div class="take">Problem: the context window is <span class="hl">finite</span>. What belongs in it? How do we manage long sessions?</div>

---

<!-- _class: compo -->

## Resend all previous input

<div class="img"><img src="../images/context-growth-quadratic-cropped.png" /></div>

<div class="take">Each call grows <span class="hl">linearly</span> → the total grows <span class="hl">quadratically</span><br/><span class="small">Every call resends the whole history: 6K + 11K + 16K + 21K + 26K = 80K after 5 calls</span></div>

---

<!-- _class: plate white -->

## Initial prompt anatomy

<div class="frame short"><img src="../images/initial-prompt-anatomy-cropped.png" /></div>

<div class="take">Your message is <span class="hl">a small part</span> of the context. What fills the rest?</div>

---

<!-- _class: anatomy -->

## Full context anatomy

<div class="grid">

<div class="c">
<div class="h"><span class="n">1</span>Base instructions</div>

- Harness system prompt

</div>

<div class="c">
<div class="h"><span class="n">2</span>Tool definitions</div>

- Built-in tools
- MCP tools

</div>

<div class="c">
<div class="h"><span class="n">3</span>Developer context</div>

- Permissions
- Developer instructions, mode
- Skills: name + description
- Memories, plugins, apps

</div>

<div class="c">
<div class="h"><span class="n">4</span>User context</div>

- AGENTS.md
- Environment: cwd, date, shell

</div>

<div class="c">
<div class="h"><span class="n">5</span>Conversation</div>

- User messages
- Assistant messages
- Reasoning items
- Tool calls + outputs

</div>

<div class="c">
<div class="h"><span class="n">6</span>Injected mid-session</div>

- Context updates
- Model switch, time, budget
- Hooks, subagents
- Compaction summary
- File-specific rules

</div>

<div class="c hidden">
<div class="h"><span class="n">7</span>Hidden by provider</div>

- Chat template tokens
- Tool schemas as text
- Provider system message

</div>

<div class="c out">
<div class="h"><span class="n">8</span>Output</div>

- Reply
- Reasoning tokens

</div>

</div>

---

<!-- _class: compo -->

## Where do the tokens go?

<div class="row">
<div class="lbl">OpenHands<span>1,500 sessions, mean 78K tokens</span></div>
<div class="img"><img src="../images/context-composition-cropped.png" /></div>
</div>

<div class="row">
<div class="lbl">My Claude Code sessions<span>from ~/.claude/projects</span></div>
<div class="img dark"><img src="../images/context-composition-my.png" /></div>
</div>

<div class="take">Tool calls + results fill <span class="hl">57–68%</span> of the window. Your prompt is a rounding error.<br><span class="small"><span class="tip">TIP</span> Clear old tool output. The context gets smaller, and the user–agent conversation stays word for word.</span></div>

---

<!-- _class: tokenomics -->

## Tokenomics: agents pay to read, not to write

<div class="k">Token type · share of all task tokens</div>

<div class="stack">
<div class="in"><b>53.9%</b>Input: prompts, tools, history</div>
<div class="rs"><b>21.6%</b>Reasoning</div>
<div class="ou"><b>24.4%</b>Output: code, text, tool calls</div>
</div>

<div class="k gap">Stage · avg share of task tokens, when the stage ran</div>

<div class="bars">
<div class="bar"><span>Code review</span><div class="fill w1">59.4%</div></div>
<div class="bar"><span>Code completion</span><div class="track"><div class="fill w2">26.8%</div><span class="note">6 of 30 tasks</span></div></div>
<div class="bar"><span>Documentation</span><div class="fill w3">20.1%</div></div>
<div class="bar"><span>Testing</span><div class="fill w4">10.3%</div></div>
<div class="bar"><span><strong>Coding</strong></span><div class="fill hot w5">8.6%</div></div>
<div class="bar"><span>Design</span><div class="fill lo w6">2.4%</div></div>
</div>

<div class="take">Code review costs <span class="hl">~7×</span> more tokens than writing the code</div>

<div class="src">ChatDev multi-agent system, GPT-5, 30 tasks · <a href="https://arxiv.org/abs/2601.14470">Salim et al., Tokenomics, arXiv 2601.14470</a></div>

---

<!-- _class: bigtitle -->

<div class="num">Demo</div>

# Eduagent Context Demo

<div class="kicker">An educational harness based on Codex: see <strong>every token</strong> the model receives.</div>

---

<!-- _class: bigtitle -->

<div class="num">1.2</div>

# Context Rot

<div class="kicker">Why quality drops and latency grows with <strong>context length</strong>.</div>

---

<!-- _class: pull -->

<div class="line rot">As context grows, the model gets <span class="hl">worse at using&nbsp;it</span></div>

<div class="sub">A model that accepts 1M tokens doesn't use 1M tokens well.<br>And <strong>every request gets slower, less accurate and more expensive</strong>.</div>

<div class="attrib">Context rot · Chroma, 2025 · Anthropic, 2025</div>

---

<!-- _class: rot -->

## Why we want long context anyway

<div class="cols3">

<div class="card">
<div class="num">// 01</div>
<div class="glyph">🏗️</div>
<div class="head">Long tasks</div>

- Migrations, large refactors
- Long autonomous runs
- Deep research

</div>

<div class="card">
<div class="num">// 02</div>
<div class="glyph">📚</div>
<div class="head">Big inputs</div>

- One big document
- Long media
- Many-shot examples

</div>

<div class="card">
<div class="num">// 03</div>
<div class="glyph">🧭</div>
<div class="head">Unknown scope</div>

- Hard, vague tasks
- You can't pick the context upfront

</div>

</div>

<div class="take">Some tasks need long context. So we must know <span class="hl">what it costs</span></div>

---

<!-- _class: rot -->

## The price of long context

<div class="grp">
<div class="g">The model gets worse</div>
<div class="g">Each request gets slower and pricier</div>

<div class="cost q"><div class="n">01</div><div class="t">Worse quality</div><div class="d">Weaker reasoning, repeated mistakes</div></div>
<div class="cost q"><div class="n">02</div><div class="t">Worse accuracy</div><div class="d">Forgets instructions, mixes up facts</div></div>
<div class="cost"><div class="n">03</div><div class="t">Slower</div><div class="d">Long wait for the first word</div></div>
<div class="cost"><div class="n">04</div><div class="t">More expensive</div><div class="d">Bills grow faster than the session</div></div>
</div>

<div class="bad">
<div class="k">Bad context makes 01 and 02 worse</div>
<div class="chips">
<div><b>Poisoning</b>A hallucination keeps being referenced</div>
<div><b>Distraction</b>The agent repeats past actions</div>
<div><b>Confusion</b>Too many tools to choose from</div>
<div><b>Clash</b>Parts of the context contradict each other</div>
</div>
</div>

<div class="src">Drew Breunig, How Long Contexts Fail, 2025</div>

---

<!-- _class: rot -->

## Why the model gets worse

<div class="cols3">

<div class="card">
<div class="num">// 01</div>
<div class="glyph">🖍️</div>
<div class="head">Fixed attention budget</div>
<div class="body">Attention weights add up to 100%. More tokens = less for each. A highlighter with a fixed amount of ink.</div>
</div>

<div class="card">
<div class="num">// 02</div>
<div class="glyph">📍</div>
<div class="head">Position bias</div>
<div class="body">Models favour the start and the end, whatever is there. The middle gets lost.</div>
</div>

<div class="card">
<div class="num">// 03</div>
<div class="glyph">🏋️</div>
<div class="head">Little practice</div>
<div class="body">Long documents are rare in training data. Models can <strong>run</strong> at 1M tokens, not <strong>use</strong> them well.</div>
</div>

</div>

<div class="src">Anthropic, Effective context engineering, 2025 · Liu et al., Lost in the Middle, 2023 · Neubig, CMU 11-768, 2026</div>

---

<!-- _class: rot -->

## Context rot in numbers

<div class="tiles">

<div class="rl">Quality<span>The model gets worse</span></div>
<div class="tile dark"><div class="big">−14–85%</div><div class="d">Scores drop from length alone, even if the extra tokens are whitespace</div><div class="s">Du et al., 2025</div></div>
<div class="tile dark"><div class="big">99 → 70%</div><div class="d">Retrieval at 32K when question and answer share no words</div><div class="s">NoLiMa, 2025</div></div>
<div class="tile dark"><div class="big">68%</div><div class="d">Best models follow only 68% of 500 instructions</div><div class="s">IFScale, 2025</div></div>

<div class="rl">Cost<span>100 steps, 20K prompt, +2K per step</span></div>
<div class="tile"><div class="big">10×</div><div class="d">Step 100 costs 10× step 1</div><div class="s">Illustrative</div></div>
<div class="tile"><div class="big">$36 → $4.4</div><div class="d">No cache vs cache. Cheaper, but still quadratic</div><div class="s">Claude API prices</div></div>
<div class="tile"><div class="big">3×</div><div class="d">Fewer tokens: 5 fresh sessions of 20 steps vs one of 100</div><div class="s">Illustrative</div></div>

</div>

<div class="take">A long session costs <span class="hl">more per step</span>. Caching makes it cheaper, not better at scale</div>

---

<!-- _class: watch big -->

## So what?

1. New task → new session. Compact or hand off with a short summary
2. Put what matters at the start or the end. Restate the goal (todo lists)
3. Correct early or start over. Don't argue with a poisoned context
4. Don't break the cache mid-session: same model, same tools

---

<!-- _class: bigtitle -->

<div class="num">1.3</div>

# Caching

<div class="kicker">The rule everything else must respect. <strong>Make-it-or-break-it</strong> for prod agents.</div>

---

<!-- _class: cache -->

## What is prompt caching?

<div class="two">

<div class="box">
<div class="k">What</div>

<strong>Save the result</strong> of an expensive computation (processing the prompt prefix) and reuse it, instead of computing it again.

</div>

<div class="box">
<div class="k">How</div>
<div class="flow">
<div class="step">Match the start of the request (the <u>prefix</u>) against recent requests</div>
<div class="hit"><b>Hit</b>Read the prefix from cache: ≤0.1× input price</div>
<div class="miss"><b>Miss</b>Compute it all, write to cache: 1.25× input price</div>
</div>
</div>

</div>

<div class="q">"The <span class="hl">KV-cache hit rate</span> is the single most important metric for a production-stage AI agent"<span class="attrib">— Yichao Ji, Manus, 2025</span></div>

---

<!-- _class: cache -->

## Why caching matters

<div class="ben">

<div class="t dark"><div class="big">10×</div><div class="h">Cheaper</div><div class="d">Cache reads cost 0.1× the input price (20× cheaper on Opus and Sonnet 5.5). A write costs 1.25×, so it pays off after one read</div><div class="s">Claude &amp; OpenAI pricing</div></div>

<div class="t"><div class="big">−67%</div><div class="h">Faster</div><div class="d">Time to first token: −7% at 1K tokens, −67% at 150K+. The longer the prompt, the bigger the win</div><div class="s">OpenAI, Prompt Caching 201</div></div>

<div class="t"><div class="big">5×</div><div class="h">More throughput</div><div class="d">Cache reads don't count toward Claude rate limits. 2M tokens/min limit + 80% hits = 10M tokens/min</div><div class="s">Claude rate limits</div></div>

<div class="t"><div class="big">0</div><div class="h">Quality cost</div><div class="d">Same model, same answer. Only the compute is reused</div><div class="s">Anthropic, OpenAI</div></div>

</div>

<div class="take">Real agent loops read a median <span class="hl">84%</span> of input from cache. Below 80%? Something breaks it</div>

<div class="src">Anthropic, Optimizing for cost and intelligence, 2026</div>

---

<!-- _class: plate short -->

## Caching visualised

<div class="frame"><img src="../images/caching-cmu-cropped.png" /></div>

<div class="note">Each call reads the cached prefix and computes only the <strong>new</strong> part</div>

<div class="note src">Neubig, CMU 11-768, 2026 · Gim et al., Prompt Cache, MLSys 2024</div>

---

<!-- _class: cache -->

## What breaks the cache

<div class="ben three">

<div class="t hot"><div class="big sm">The prefix changes</div><div class="d">Everything after the change is computed again</div>

- Edit the system prompt or an old message
- Add or remove tools: MCP server, plugin
- Compact the conversation
- Many images in the history
- Upgrade the harness

</div>

<div class="t dark"><div class="big sm">A different cache</div><div class="d">Same prefix, but no cache for it yet</div>

- Switch the model: each model has its own cache
- Change the effort level (fixed on GPT-6 and Claude 5.5, native API only)

</div>

<div class="t"><div class="big sm">Time runs out</div><div class="d">The TTL counts from the start of the request</div>

- Claude: 5 min, or 1 h for 2× the write price
- OpenAI GPT-6: 30 min
- Earlier OpenAI: 5–10 min, up to 24&nbsp;h extended

</div>

</div>

<div class="take">One model switch at 220K tokens ≈ <span class="hl">11 cached steps</span> of cost</div>

---

<!-- _class: plate miss -->

## Cache miss: change the prefix, pay for everything again

<div class="frame"><img src="../images/caching-claude.png" /></div>

<div class="note">A change anywhere <strong>invalidates everything after it</strong>, even content that did not change</div>

---

<!-- _class: cache -->

## Three ways to cache

<div class="ben three">

<div class="t dark"><div class="big sm">Implicit</div><div class="h">Provider decides</div><div class="d">The provider caches common prefixes. You change nothing. Best effort: no hit is guaranteed</div><div class="tag">OpenAI · Gemini</div></div>

<div class="t"><div class="big sm">Breakpoints</div><div class="h">You mark the prefix</div><div class="d">A marker on a block: "cache everything up to here". The next request reads the longest entry that still matches. Usually up to 4 markers</div><div class="tag">Claude · Bedrock · OpenAI GPT-5.6+</div></div>

<div class="t"><div class="big sm">Cache objects</div><div class="h">You upload once</div><div class="d">Upload the content, get a cache ID, refer to it later. You pay for storage per hour until the TTL ends</div><div class="tag">Gemini</div></div>

</div>

<div class="take">Agents use the first two: a growing chat needs a prefix that <span class="hl">moves forward</span></div>

---

<!-- _class: plate trap -->

## Cache-cost trap: short prefixes are not cached

<div class="frame"><img src="../images/cache-cost-trap-cropped.png" /></div>

<div class="note">Below 1,024 tokens nothing is cached: a <strong>1,000-token</strong> prefix costs more than a <strong>2,000-token</strong> one</div>

<div class="note src">OpenAI, Prompt caching guide · minimum 1,024 tokens · read 0.1× · write 1.25× · 9 reads per write</div>

---

<!-- _class: cache -->

## Best practices: append, don't edit

<div class="ben">

<div class="t dark"><div class="h">01 Stabilize the prefix</div>

- Static first, dynamic last
- Pick model and effort at the start
- No tool changes mid-task

</div>

<div class="t"><div class="h">02 Append new state</div>

- New info goes in new messages
- Rewind, don't argue: the old cache still works
- Compact at natural breaks

</div>

<div class="t"><div class="h">03 Keep it warm</div>

- 1 h TTL if you pause often
- Pre-warm for low latency
- A 4-min answer leaves ~1 min of a 5-min TTL

</div>

<div class="t"><div class="h">04 Measure reuse</div>

- Watch the cache hit rate
- Aim for 80%+
- A drop means something broke the prefix

</div>

</div>

<div class="take">Rule of thumb: <span class="hl">append, don't edit</span>. Pay for a cache break only at a natural break</div>

---

<!-- _class: bigtitle -->

<div class="num">1.4</div>

# Context Engineering

<div class="kicker">The smallest set of <strong>high-signal tokens</strong> for the next step. Four strategies, shown live on a real repo.</div>

---

<!-- _class: ce -->

## What is context engineering?

<div class="def">Caching makes long context <strong>cheaper</strong><br>Context engineering makes it <strong>smaller</strong></div>

<div class="quotes">
<div class="qc"><div>"Finding the <span class="hl">smallest possible set of high-signal tokens</span> that maximize the likelihood of some desired outcome"</div><span class="attrib">— Anthropic</span></div>
<div class="qc"><div>"The delicate art and science of filling the context window with <span class="hl">just the right information</span> for the next step"</div><span class="attrib">— Andrej Karpathy</span></div>
<div class="qc"><div>"The art of providing all the context for the task to be <span class="hl">plausibly solvable</span> by the LLM"</div><span class="attrib">— Tobi Lütke, Shopify</span></div>
</div>

<div class="vs">
<div><b>Prompt engineering</b>Tailor the input for <u>one</u> model response</div>
<div class="arrow">→</div>
<div class="on"><b>Context engineering</b>Build a system that gives the model the right information over <u>many</u> turns</div>
</div>

---

<!-- _class: plate pce -->

<div class="frame"><img src="../images/prompt-vs-context-engineering.png" /></div>

<div class="note src">Anthropic, Effective context engineering for AI agents, 2025</div>

---

<!-- _class: ce -->

## Four strategies of context engineering

<div class="moves">

<div class="m">
<div class="n">// 01</div>
<div class="v">✍️ Write</div>
<div class="d">Save information outside the context window</div>

- Todo list
- Handoff file
- Memory files

<div class="loss"><b>Loses</b><br/>Freshness: memory goes stale<br/>&nbsp;</div>
</div>

<div class="m">
<div class="n">// 02</div>
<div class="v">🎯 Select</div>
<div class="d">Pull in only what the next step needs</div>

- AGENTS.md vs skills
- Search: grep, graph
- Only the matches from big output

<div class="loss"><b>Loses</b><br/>What the agent doesn't know to ask for</div>
</div>

<div class="m">
<div class="n">// 03</div>
<div class="v">✂️ Compress</div>
<div class="d">Fewer tokens for the same information</div>

- Filter output at the source
- Clear old tool outputs
- Compaction

<div class="loss"><b>Loses</b><br/>Details, and you can't see which</div>
</div>

<div class="m">
<div class="n">// 04</div>
<div class="v">📦 Isolate</div>
<div class="d">Do heavy work in another window</div>

- Subagents
- Code execution

<div class="loss"><b>Loses</b><br/>The parent's context at the handoff</div>
</div>

</div>

<div class="src">LangChain, Context Engineering for Agents, 2025 · Anthropic, Effective context engineering, 2025</div>

---

<!-- _class: ce -->

## Running example: working on a big, unfamiliar repo

<div class="setting">

<div class="col big">
<div class="k">The repo: pi<span>github.com/earendil-works/pi</span></div>

- A coding-agent harness: TypeScript monorepo, 11 packages, ~410K lines
- CI is red: 55 of the last 100 runs failed. One failed job log ≈ 115K tokens
- AGENTS.md and CONTRIBUTING.md: ~230 lines of rules
- **pi is only the repo. The agent is Claude Code**

</div>

<div class="col big panels">
<div class="k">What to watch<span>quantext: rebuilds every call from the session log</span></div>
<div class="p"><b>Context</b>What each call holds, by category, and how it was billed</div>
<div class="p"><b>Changed</b>What changed since the last call. Cache breaks, and why</div>
<div class="p"><b>Tools</b>Output tokens of each tool call, and its lifetime cost</div>
<div class="p"><b>Compact</b>What a compaction kept, removed and summarised</div>
</div>

</div>

---

<!-- _class: ce -->

<div class="movehead"><span class="n">// 01</span><span class="v">✍️ Write</span><span class="d">Save information outside the context window</span></div>

<div class="problem"><span class="k">Problem</span>The context window is temporary: it fills up, sessions end, compaction drops details</div>

<div class="lv">

<div class="col big">
<div class="k">A · Task memory<span>Lives until the task is done</span></div>

- **Todo list** - the plan, updated at each step
- **Handoff file** - progress for a fresh session

</div>

<div class="col big dark">
<div class="k">B · Long-term memory<span>Lives across tasks</span></div>

- **Human-written** - `AGENTS.md` / `CLAUDE.md`, always loaded
- **Agent-written during work** - Claude Code auto memory
- **Consolidated offline** - a background job merges old sessions: Codex memories

</div>

</div>

<div class="src">Manus, 2025 · Anthropic, Effective harnesses for long-running agents, 2025 · LangChain, 2025</div>

---

<!-- _class: ce -->

## Write: two ways to remember

<div class="lv">

<div class="col">
<div class="k">📝 Claude Code auto memory<span>Notes during the day</span></div>

- **Who writes** - the main agent, during the session, with its file tools
- **At start** - first 200 lines or 25 KB of `MEMORY.md`, the index
- **On demand** - topic files, read with file tools
- **Scope** - per git repo. On by default

</div>

<div class="col dark">
<div class="k">🌙 Codex memories<span>A diary written at night</span></div>

- **Who writes** - a background job: one LLM call per idle session (6 h+), then a sub-agent merges the notes
- **At start** - `memory_summary.md`, cut to 2,500 tokens
- **On demand** - grep `MEMORY.md` and rollout summaries
- **Scope** - global per user. Off by default

</div>

</div>

<div class="sub">Kinds of memory</div>

<div class="tiles three">
<div class="tile"><div class="big">Semantic</div><div class="d">Facts: "user prefers uv", project structure</div></div>
<div class="tile"><div class="big">Episodic</div><div class="d">Past experiences: "last time this test failed because…"</div></div>
<div class="tile"><div class="big">Procedural</div><div class="d">How to do things: AGENTS.md rules, skills</div></div>
</div>

<div class="take">Both use the same trick: a <span class="hl">small index upfront</span>, details on demand. That is Select</div>

<div class="src">CoALA, Sumers et al., 2023 · Claude Code memory docs · Codex source</div>

---

<!-- _class: ce -->

## Write: memory goes stale

<div class="flow">
<div class="st"><b>Session 1</b>Learns: "run tests with <code>npm test</code> in packages/agent"</div>
<div class="st dark"><b>Auto memory</b>The agent writes a note and links it in <code>MEMORY.md</code></div>
<div class="st"><b>Session 2</b>The index is loaded upfront. The fact helps</div>
<div class="st"><b>The repo changes</b>The test script is renamed</div>
<div class="st hot"><b>Session 3</b>Follows the old fact: wasted steps, or a wrong fix</div>
</div>

<div class="lv gap">

<div class="col big dark">
<div class="k">Poisoning that persists<span>across sessions</span></div>

- A wrong note is read at the start of every session
- The agent trusts it more than the code

</div>

<div class="col big">
<div class="k">What helps</div>

- Look at the memory files now and then. Delete wrong ones
- Memory says *where to look*, the repo says *what is true*

</div>

</div>

<div class="demo extra"><span class="tag">Demo</span><span>The Memory page in quantext, then session 2: find <code>MEMORY.md</code> in the injected context</span></div>

---

<!-- _class: ce -->

## Write: the todo list lives outside the context

<div class="flow">
<div class="st dark"><b>1 · Model</b><code>TaskCreate</code> per step, <code>TaskUpdate</code> with only the new status</div>
<div class="st"><b>2 · Harness</b>Stores the list outside the context, shows it in the UI</div>
<div class="st hot"><b>3 · Later</b>Tasks not touched for a while? The harness injects the list at the end of the context</div>
</div>

<div class="lv gap">

<div class="col big">
<div class="k">Pros</div>

- The goal comes back at the end, where attention is strongest
- Cheap: small calls, no full plan in every update
- Survives compaction: the list is not in the history

</div>

<div class="col big">
<div class="k">Cons</div>

- Works only if the model keeps it up to date
- The reminders add tokens
- Not always on: off by default for Claude 5 models in interactive mode

</div>

</div>

<div class="note"><strong>Codex is different:</strong> <code>update_plan</code> sends the full plan every time, and nothing is injected. The newest copy is just near the end of the history</div>

<div class="demo"><span class="tag">Demo</span><span>First look at quantext: <code>TaskCreate</code> and <code>TaskUpdate</code> in Tool calls</span></div>

---

<!-- _class: ce -->

## Write: hand off to a fresh session

<div class="cmp">

<div>

```
# PROGRESS.md
Goal:  fix the failing test in packages/agent
Done:  cause found: <file:line>, <why>
Open:  is the retry flaky on CI only?
Next:  run `npm test` in packages/agent
Files: src/agent-loop.ts, test/loop.test.ts
```

</div>

<div class="col big">
<div class="k">Three steps</div>

- "Write PROGRESS.md: goal, done, open, next step, key files"
- `/clear` (Claude Code) or `/new` (Codex)
- "Continue from PROGRESS.md"

</div>

</div>

<div class="note"><strong>Compaction is an automatic handoff.</strong> Codex's compaction prompt asks for "a handoff summary for another LLM". Your own file is a handoff that you can read, edit and keep</div>

<div class="demo extra"><span class="tag">Demo</span><span>Handoff, then <code>/clear</code>. <b>Compare the two sessions</b>: context size and cost per call</span></div>

---

<!-- _class: ce -->

## Write: what it costs, and what to do

<div class="costs">
<div class="k">What Write costs</div>
<div class="chips">
<div><b>Read back</b>A note helps only if it is read at the right time. That is a Select question</div>
<div><b>Stale</b>Wrong memory = poisoning that persists across sessions</div>
<div><b>Leaks</b>Memory can leak into unrelated tasks</div>
<div><b>Who writes</b>Agent: spends attention mid-task. Offline job: free, but arrives late</div>
</div>
</div>

<div class="daily">
<div class="k">In your daily work</div>

- Ask for a todo list on long tasks. Check that the agent keeps it up to date
- End a long session with a handoff file, then start a fresh one
- Look at what your agent remembers. Prune it

</div>

---

<!-- _class: ce -->

<div class="movehead"><span class="n">// 02</span><span class="v">🎯 Select</span><span class="d">Pull in only what the next step needs</span></div>

## Select: who picks the context, and when

<div class="problem"><span class="k">Problem</span>The agent can't use what it doesn't see, and everything it sees costs tokens and attention</div>

<div class="lv">

<div class="col big">
<div class="k">A · Upfront<span>The harness selects, before the call</span></div>

- `AGENTS.md`, `@file`, skill descriptions, classic RAG
- **Plus:** always there, cheap, predictable
- **Minus:** paid in every request, even when not needed

</div>

<div class="col big dark">
<div class="k">B · On demand<span>The agent selects, at runtime</span></div>

- grep / glob / read, skill bodies, tool search
- **Plus:** only what the task asks for
- **Minus:** more turns, and it misses what it doesn't know to ask for

</div>

</div>

<div class="take">Most agents mix both: a <span class="hl">small index upfront</span>, details on demand</div>

---

<!-- _class: ce -->

## Select: always loaded vs progressive disclosure

<div class="lv">

<div class="col big dark">
<div class="k">AGENTS.md<span>Always loaded</span></div>

- Every token in every request
- 300 lines ≈ 4K tokens × 50 requests = **200K input tokens** per session
- The cache makes it cheaper, but it still takes attention

</div>

<div class="col big">
<div class="k">Skill<span>Progressive disclosure</span></div>

- Always: name + description, ~50 tokens
- When the task needs it: the `SKILL.md` body
- Only if needed: bundled files and scripts

</div>

</div>

<div class="sub">The same pattern in three places</div>

<div class="chain big">
<div class="lbl">Skills</div><div class="s first">name + description</div><div class="a">→</div><div class="s">SKILL.md body</div><div class="a">→</div><div class="s">bundled files</div>
<div class="lbl">Tools</div><div class="s first">tool search stub</div><div class="a">→</div><div class="s">full definition (−85% tokens)</div><div class="a">→</div><div class="s">CLI <code>--help</code></div>
<div class="lbl">Memory</div><div class="s first">memory_summary.md</div><div class="a">→</div><div class="s">grep MEMORY.md</div><div class="a">→</div><div class="s">rollout summaries</div>
</div>

<div class="demo"><span class="tag">Demo</span><span>pi's rules in CLAUDE.md vs as a skill, on a task that doesn't need them. <b>Compare the injected context and the cost</b></span></div>

---

<!-- _class: ce -->

## Select: how the agent finds code

<div class="axes big three">
<div class="h"></div>
<div class="h">Keyword: grep, paths</div>
<div class="h">Structure: AST, graph</div>
<div class="h">Semantic: embeddings</div>

<div class="r">Upfront<span>harness</span></div>
<div><b>AGENTS.md, @file</b>Always there, predictable</div>
<div><b>Aider repo map</b>Key symbols of the repo in the prompt</div>
<div><b>Classic RAG</b>Top-k chunks for the query</div>

<div class="r">On demand<span>agent</span></div>
<div class="cc"><b>Claude Code, Codex</b>grep / glob / read, refine the query</div>
<div><b>graphify</b>query · path A B · explain, on a code graph</div>
<div><b>Cursor semantic search</b>A tool, +12.5% accuracy on top of grep</div>
</div>

<div class="note"><strong>grep is the default, and it works well.</strong> graphify claims −80% tokens. On pi (39K nodes) its path from <code>coding-agent</code> to the provider went through re-exports, not the call chain: measure on your own repo</div>

---

<!-- _class: ce -->

## Select: big output, pull in only what you need

<div class="paths">

<div class="path bad">
<div class="n">// 01</div>
<div class="h">MCP tool</div>

```
get_job_logs(job_id)
```

<div class="in"><b>~115K-token log</b>Too big: Claude Code saves it to a file, the model gets a path and "use jq". <b>7 turns · $0.11</b></div>
</div>

<div class="path">
<div class="n">// 02</div>
<div class="h">CLI + pipe</div>

```
gh api …/jobs/<id>/logs \
  | grep -A12 "FAIL "
```

<div class="in"><b>Only the matches</b>The shell filters before the model reads anything. <b>2 turns · $0.06</b></div>
</div>

<div class="path">
<div class="n">// 03</div>
<div class="h">CLI → file → search</div>

```
gh api …/jobs/<id>/logs > ci.log
grep -n "FAIL " ci.log
```

<div class="in"><b>A path + matches</b>The log stays on disk (Write). Read more later. <b>3 turns · $0.07</b></div>
</div>

</div>

<div class="note"><strong>Harnesses now offload big results by themselves, but it costs turns.</strong> A direct pipe: 3× fewer turns, half the cost. "Code mode" lets the agent call MCP tools from code, if the harness supports it</div>

<div class="demo"><span class="tag">Demo</span><span>A failed CI run of pi, three ways. <b>Compare turns and cost</b>, then open Tool calls</span></div>

---

<!-- _class: ce -->

## Select: what it costs, and what to do

<div class="costs">
<div class="k">What Select costs</div>
<div class="chips">
<div><b>Slower</b>On demand = more turns, and each result adds tokens</div>
<div><b>Unknown unknowns</b>A weak skill or tool description = never loaded</div>
<div><b>Noise</b>Wrong chunks distract. Stale indexes give old code</div>
<div><b>Cache</b>Changing loaded tools breaks it. Mask, don't remove</div>
</div>
</div>

<div class="daily">
<div class="k">In your daily work</div>

- Keep AGENTS.md short: only what every task needs. Move the rest into skills
- Write skill descriptions that say <u>when</u> to use the skill
- Pipe big output, or save it to a file and grep it. Avoid big MCP results
- Turn off MCP servers and tools that you don't use

</div>

<div class="src">Anthropic, 2025 · Pragmatic Engineer, Building Claude Code, 2026 · Cursor, Semantic search, 2025 · Aider, Repository map · graphify</div>

---

<!-- _class: ce -->

<div class="movehead"><span class="n">// 03</span><span class="v">✂️ Compress</span><span class="d">Fewer tokens for the same information</span></div>

## Compress: where we cut

<div class="problem"><span class="k">Problem</span>Tool calls and results fill 57–68% of the window, and every output is sent again on every later call</div>

<div class="lv three">

<div class="col big">
<div class="k">A · At the source<span>Before tokens enter</span></div>

- Filters for command output: RTK
- Token-efficient tools: pagination, filters
- Harness caps: Claude Code 25K per tool

</div>

<div class="col big dark">
<div class="k">B · Discard<span>In the history, no LLM</span></div>

- Clear old tool outputs, keep the calls
- Same for old thinking blocks
- Restorable, if the output is on disk

</div>

<div class="col big">
<div class="k">C · Condense<span>In the history, LLM, lossy</span></div>

- Compaction: summarise, start again with the summary
- Steer it: `/compact <focus>`
- Codex on OpenAI: an encrypted item you can't read

</div>

</div>

<div class="src">Anthropic, Writing tools for agents, 2025 · RTK · Claude Code docs · OpenAI Compaction docs</div>

---

<!-- _class: ce -->

## Compress at the source: filter tool output

<div class="lv">

<div class="col big">
<div class="k">RTK: a CLI proxy<span>github.com/rtk-ai/rtk</span></div>

- `git status`: a 3-line summary instead of 40 lines
- `npm test` / `pytest`: failures only, passes as a count
- `git diff`, `git log`: less context, one line per commit
- `ls` / `grep`: grouped by file, long lines cut

</div>

<div class="col big dark">
<div class="k">Good to know</div>

- 90% less output ≠ 90% less cost: output is one part of the input
- Filters before output enters the context, so no cache break
- `rtk bypass <cmd>` gives the raw output
- Setup: `rtk init -g` adds a Claude Code hook that rewrites `git status` to `rtk git status`

</div>

</div>

<div class="demo extra"><span class="tag">Demo</span><span>The same steps (<code>npm test</code>, <code>git status</code>, <code>git diff</code>) with and without RTK, then <code>rtk gain</code></span></div>

---

<!-- _class: ce -->

## Discard vs condense: what the model sees after

<div class="ba">

<div>
<div class="colh">Before<span>a long session</span></div>
<div class="it sys">System prompt + tools</div>
<div class="it sys">CLAUDE.md, memory, environment</div>
<div class="it">User: "Why does CI fail?"</div>
<div class="it tool">Tool call + output, 8K</div>
<div class="it tool">Tool call + output, 6K</div>
<div class="it">Assistant: "The cause is…"</div>
<div class="it tool">Tool call + output, 5K</div>
<div class="it">User: "Fix it"</div>
</div>

<div>
<div class="colh">After clear<span><code>/clear-tool-outputs keep 1</code></span></div>
<div class="it sys">System prompt + tools</div>
<div class="it sys">CLAUDE.md, memory, environment</div>
<div class="it">User: "Why does CI fail?"</div>
<div class="it cleared">Tool call + [Old tool result content cleared]</div>
<div class="it cleared">Tool call + [Old tool result content cleared]</div>
<div class="it">Assistant: "The cause is…"</div>
<div class="it tool">Tool call + output, 5K</div>
<div class="it">User: "Fix it"</div>
<div class="cost">All messages word for word. <b>0 LLM calls.</b> The cache breaks at the first cleared output</div>
</div>

<div>
<div class="colh">After compaction<span><code>/compact</code></span></div>
<div class="it sys">System prompt + tools</div>
<div class="it sys">CLAUDE.md, memory, environment (again)</div>
<div class="it sum">Summary: "This session is being continued from a previous conversation…"</div>
<div class="it">Recent files, todo list (attached again)</div>
<div class="cost">All messages, tool calls and outputs are replaced by the summary. <b>1 LLM call</b>, a new prefix, lost details</div>
</div>

</div>

<div class="demo"><span class="tag">Demo</span><span>One session: <code>/clear-tool-outputs</code>, then <code>/compact</code>. Then ask about an early detail</span></div>

---

<!-- _class: ce -->

## Compress: simple beats clever

<div class="tiles three">
<div class="tile dark"><div class="big">½ cost</div><div class="d">Observation masking vs LLM summary. Same solve rate</div><div class="s">JetBrains, NeurIPS 2025</div></div>
<div class="tile"><div class="big">−84%</div><div class="d">Tokens in a 100-turn eval with context editing, +29% on agentic search</div><div class="s">Anthropic, 2025</div></div>
<div class="tile"><div class="big">0 LLM calls</div><div class="d">Masking is free. Summary costs a call and a buffer in the window</div><div class="s">Claude Code, 2026</div></div>
</div>

<div class="bar"><b>Hybrid</b>Mask first, summarise only when masking is not enough: −7% cost vs masking, −11% vs summary</div>

<div class="lv gap">

<div class="col big">
<div class="k">Never remove<span>What the next step needs</span></div>

- **Errors and stack traces** - so the agent doesn't repeat them
- **The plan** and the user's instructions
- **The last N tool results** - the fresh tail

</div>

<div class="col big">
<div class="k">Cache-friendly<span>Clearing and compaction break the prefix</span></div>

- Clear in big chunks (`clear_at_least`)
- Compact at natural breaks, not mid-step
- Summary call: a cache-safe fork, same prefix

</div>

</div>

<div class="src">JetBrains, The Complexity Trap, NeurIPS 2025 · Claude API, Context editing · Claude Code docs</div>

---

<!-- _class: ce -->

## Compress: what it costs, and what to do

<div class="costs">
<div class="k">What Compress costs</div>
<div class="chips">
<div><b>Lost details</b>You can't see which. Back only if the raw data is on disk</div>
<div><b>New prefix</b>After compaction, only the system prompt and tools stay cached</div>
<div><b>Cache break</b>Clearing breaks the cache from the first cleared output</div>
<div><b>Summary call</b>Compaction costs one more LLM call</div>
</div>
</div>

<div class="daily">
<div class="k">In your daily work</div>

- Filter tool output at the source: RTK, `--quiet`, `| tail`
- Clear old tool output at natural breaks. In Claude Code: a plugin, e.g. quantext `/clear-tool-outputs`
- `/compact <focus>` at natural breaks. New task → new session

</div>

---

<!-- _class: ce -->

<div class="movehead"><span class="n">// 04</span><span class="v">📦 Isolate</span><span class="d">Do heavy work in another window</span></div>

## Isolate: subagents

<div class="q">"The essence of search is compression": read tens of thousands of tokens, return 1–2K<span class="attrib">— Anthropic, multi-agent research</span></div>

<div class="moves">

<div class="m dark">
<div class="n">// 01</div>
<div class="d">🔎 Explorer (read-only)</div>

- Reads a lot, returns a summary
- Claude Code Explore on Haiku
- Lead + subagents beat one Opus by 90%

</div>

<div class="m">
<div class="n">// 02</div>
<div class="d">🧐 Clean reviewer</div>

- Never saw the build: no bias
- Coder and reviewer share no context

</div>

<div class="m">
<div class="n">// 03</div>
<div class="d">⚡ Parallel workers</div>

- Independent subtasks at once
- Up to 90% faster research
- Writes stay single-threaded

</div>

<div class="m">
<div class="n">// 04</div>
<div class="d">🔀 Another model</div>

- A model switch breaks the cache
- Use a subagent with a handoff

</div>

</div>

<div class="knobs">
<div class="lbl">Design knobs</div>
<div><b>Context in</b>Fresh brief (goal, output format, tools, limits) or fork of the parent: shares the cache</div>
<div><b>Context out</b>Summary, or files + a reference back. Avoid the "game of telephone"</div>
<div><b>Permissions</b>Read-only is the safe default</div>
</div>

<div class="demo extra"><span class="tag">Demo</span><span>An Explore subagent: quantext shows it as its own lane. <b>Its tokens vs the summary</b> that comes back to the parent</span></div>

<div class="src">Anthropic, How we built our multi-agent research system, 2025 · Cognition, Multi-Agents: What's Actually Working, 2026 · Thariq Shihipar, 2026</div>

---

<!-- _class: ce -->

## Isolate: code execution, and the price

<div class="sub top">Outside the LLM: the agent writes a script, only the final output enters the context. The same idea as the shell pipe in Write</div>

<div class="tiles three">
<div class="tile dark"><div class="big">150K → 2K</div><div class="d">Tokens with MCP tools as code files</div><div class="s">Anthropic, 2025</div></div>
<div class="tile"><div class="big">−37%</div><div class="d">Tokens with programmatic tool calling</div><div class="s">Anthropic, 2025</div></div>
<div class="tile"><div class="big">+8%</div><div class="d">Cost for strictly sequential calls (τ²-bench). No fan-out, no gain</div><div class="s">Claude API docs</div></div>
</div>

<div class="sub">What Isolate costs</div>

<div class="tiles">
<div class="tile hot"><div class="big">4× / 15×</div><div class="d">Tokens: agents vs chat, multi-agent vs chat</div><div class="s">Anthropic, 2025</div></div>
<div class="tile"><div class="big">Handoff</div><div class="d">The subagent doesn't see the parent. The parent sees only the summary</div></div>
<div class="tile"><div class="big">Coding</div><div class="d">"Fewer truly parallelizable tasks than research"</div></div>
<div class="tile"><div class="big">Overhead</div><div class="d">Container start, script writing. Pays off only with fan-out or big results</div></div>
</div>

<div class="daily">
<div class="k">In your daily work</div>

- Give exploration and review to a subagent. Keep your main context for the build

</div>

---

<!-- _class: ce -->

## Which strategy is it?

<div class="ask"><span class="k">ASK THE ROOM</span>Shout the strategy: Write, Select, Compress or Isolate</div>

<div class="quiz">
<div class="qi"><div class="f"><code>/compact</code><span>Claude Code, Codex</span></div><div class="a q">?</div></div>
<div class="qi"><div class="f">CLAUDE.md<span>always loaded</span></div><div class="a q">?</div></div>
<div class="qi"><div class="f">Explore subagent<span>Claude Code</span></div><div class="a q">?</div></div>
<div class="qi"><div class="f">Skills<span>name + description first</span></div><div class="a q">?</div></div>
<div class="qi"><div class="f">RTK<span>filters <code>git status</code></span></div><div class="a q">?</div></div>
<div class="qi"><div class="f">PROGRESS.md<span>for a fresh session</span></div><div class="a q">?</div></div>
<div class="qi"><div class="f">Tool search<span>deferred tool stubs</span></div><div class="a q">?</div></div>
<div class="qi"><div class="f"><code>&gt; ci.log</code><span>then grep it</span></div><div class="a q">?</div></div>
</div>

---

<!-- _class: ce -->

## Which strategy is it?

<div class="ask"><span class="k">ASK THE ROOM</span>Shout the strategy: Write, Select, Compress or Isolate</div>

<div class="quiz">
<div class="qi"><div class="f"><code>/compact</code><span>Claude Code, Codex</span></div><div class="a">✂️ Compress</div></div>
<div class="qi"><div class="f">CLAUDE.md<span>always loaded</span></div><div class="a">✍️ Write + 🎯 Select</div></div>
<div class="qi"><div class="f">Explore subagent<span>Claude Code</span></div><div class="a">📦 Isolate</div></div>
<div class="qi"><div class="f">Skills<span>name + description first</span></div><div class="a">🎯 Select</div></div>
<div class="qi"><div class="f">RTK<span>filters <code>git status</code></span></div><div class="a">✂️ Compress</div></div>
<div class="qi"><div class="f">PROGRESS.md<span>for a fresh session</span></div><div class="a">✍️ Write</div></div>
<div class="qi"><div class="f">Tool search<span>deferred tool stubs</span></div><div class="a">🎯 Select</div></div>
<div class="qi"><div class="f"><code>&gt; ci.log</code><span>then grep it</span></div><div class="a">✍️ Write + 🎯 Select</div></div>
</div>

---

<!-- _class: ce -->

## Constraint for all four: the cache

| Technique                  | Cache effect                               | Cache-friendly way                                  |
| -------------------------- | ------------------------------------------ | --------------------------------------------------- |
| Write: files, notes, todo  | None, appended as new messages             | Updates go in messages, not in the system prompt    |
| Select: add/remove tools   | Breaks all of it, tools are near the start | Mask, don't remove. Tool search with deferred stubs |
| Select: on-demand loading  | None, results are appended                 | -                                                   |
| Compress: filter at source | None, filtered before it enters            | -                                                   |
| Compress: clearing         | Breaks from the first cleared result       | Clear in big chunks (`clear_at_least`)              |
| Compress: compaction       | New history = new prefix                   | Cache-safe fork for the summary call                |
| Isolate: subagent          | Fresh brief = its own new cache            | Fork shares the parent's prefix                     |
| Isolate: another model     | Each model has its own cache               | Subagent with a handoff, not a mid-session switch   |

<div class="take">Append, don't edit. Pay for a cache break only <span class="hl">when it removes many tokens</span></div>

<div class="src">Manus, 2025 · Claude API, Context editing · Thariq Shihipar, Prompt caching is everything, 2026</div>

---

<!-- _class: tk -->

## Takeaways

<div class="one"><span class="k">If you keep only one</span>The context window is the agent's working memory. Everything in it costs money, time and attention, so put in only what the next step needs</div>

<div class="rows">
<div class="n">01</div><div class="c">The model sees far more than you typed, on every call</div><div class="a">→ Run <code>/context</code> once and look</div>
<div class="n">02</div><div class="c">More context isn't free: worse answers, quadratic cost</div><div class="a">→ 1M is a limit, not a target</div>
<div class="n">03</div><div class="c">Caching is the rule everything else must respect</div><div class="a">→ Same model, same tools. Append, don't edit</div>
<div class="n">04</div><div class="c">Write: the context window is temporary</div><div class="a">→ A todo list for long tasks. A handoff file at the end</div>
<div class="n">05</div><div class="c">Select: everything you load is paid in every request</div><div class="a">→ Short AGENTS.md, skills, only the matches from big output</div>
<div class="n">06</div><div class="c">Compress: tool output is the main cost driver</div><div class="a">→ Filter at the source, clear old output, compact at breaks</div>
<div class="n">07</div><div class="c">Isolate: heavy reading goes on the side</div><div class="a">→ Subagents for exploration and review</div>
<div class="n">08</div><div class="c">Every technique throws something away</div><div class="a">→ Keep spec, progress and notes on disk</div>
</div>

---


<!-- _class: closing -->

<div class="stamp">End of Part 1</div>

# Q&amp;A

---

<!-- _class: bigtitle -->

<div class="num">Part 2</div>

# Workshop

<div class="kicker">Build &amp; compete: <strong>manage context</strong> for trader agents.</div>
