<!doctype html>
<html lang="zh-CN">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>智维工场 AI预测性维护平台</title>
  <style>
    :root {
      color-scheme: dark;
      --bg: #070c10;
      --bg-deep: #020406;
      --ink: #e6edf7;
      --muted: #93a4ba;
      --panel: rgba(10, 18, 22, 0.88);
      --panel-2: rgba(14, 24, 29, 0.8);
      --panel-3: rgba(5, 9, 13, 0.94);
      --line: rgba(91, 166, 179, 0.24);
      --line-strong: rgba(57, 189, 248, 0.48);
      --blue: #38bdf8;
      --teal: #2dd4bf;
      --green: #22c55e;
      --amber: #f59e0b;
      --red: #fb7185;
      --violet: #a78bfa;
      --soft-blue: rgba(56, 189, 248, 0.15);
      --soft-teal: rgba(45, 212, 191, 0.14);
      --soft-green: rgba(34, 197, 94, 0.14);
      --soft-amber: rgba(245, 158, 11, 0.16);
      --soft-red: rgba(251, 113, 133, 0.16);
      --soft-violet: rgba(167, 139, 250, 0.16);
      --shadow: 0 18px 46px rgba(0, 0, 0, 0.36);
      --shadow-soft: 0 10px 30px rgba(0, 0, 0, 0.26);
      --glow-blue: 0 0 22px rgba(56, 189, 248, 0.2);
      --glow-teal: 0 0 24px rgba(45, 212, 191, 0.18);
      font-family: "Fira Sans", "Microsoft YaHei", "PingFang SC", "Segoe UI", Arial, sans-serif;
    }

    * {
      box-sizing: border-box;
    }

    ::selection {
      background: rgba(56, 189, 248, 0.32);
      color: #f8fafc;
    }

    * {
      scrollbar-color: rgba(56, 189, 248, 0.45) rgba(7, 17, 31, 0.72);
      scrollbar-width: thin;
    }

    *::-webkit-scrollbar {
      width: 10px;
      height: 10px;
    }

    *::-webkit-scrollbar-track {
      background: rgba(7, 17, 31, 0.72);
    }

    *::-webkit-scrollbar-thumb {
      background: rgba(56, 189, 248, 0.42);
      border: 2px solid rgba(7, 17, 31, 0.72);
      border-radius: 999px;
    }

    body {
      margin: 0;
      background:
        radial-gradient(circle at 18% 8%, rgba(56, 189, 248, 0.16), transparent 28%),
        radial-gradient(circle at 86% 18%, rgba(45, 212, 191, 0.12), transparent 30%),
        radial-gradient(circle at 74% 82%, rgba(245, 158, 11, 0.08), transparent 28%),
        linear-gradient(180deg, #07141a 0, var(--bg-deep) 420px, var(--bg) 100%);
      color: var(--ink);
      min-height: 100vh;
      overflow-x: hidden;
      -webkit-font-smoothing: antialiased;
      text-rendering: optimizeLegibility;
    }

    html {
      overflow-x: hidden;
    }

    body::before {
      content: "";
      position: fixed;
      inset: 0;
      pointer-events: none;
      z-index: -1;
      background-image:
        linear-gradient(rgba(148, 163, 184, 0.06) 1px, transparent 1px),
        linear-gradient(90deg, rgba(148, 163, 184, 0.06) 1px, transparent 1px);
      background-size: 38px 38px;
      mask-image: linear-gradient(180deg, rgba(0, 0, 0, 0.9), transparent 82%);
    }

    button,
    input,
    select {
      font: inherit;
    }

    button {
      cursor: pointer;
    }

    .app {
      min-height: 100vh;
      display: grid;
      grid-template-columns: 260px minmax(0, 1fr);
      max-width: 100%;
      overflow-x: hidden;
    }

    .sidebar {
      background:
        linear-gradient(180deg, rgba(8, 20, 24, 0.98), rgba(2, 4, 6, 0.98)),
        linear-gradient(150deg, rgba(56, 189, 248, 0.12), transparent 42%),
        linear-gradient(25deg, rgba(245, 158, 11, 0.07), transparent 46%);
      color: #e6edf7;
      padding: 22px 18px;
      display: flex;
      flex-direction: column;
      gap: 20px;
      position: sticky;
      top: 0;
      height: 100vh;
      border-right: 1px solid rgba(56, 189, 248, 0.2);
      box-shadow: 18px 0 46px rgba(0, 0, 0, 0.24);
    }

    .brand {
      display: flex;
      gap: 12px;
      align-items: center;
      padding-bottom: 18px;
      border-bottom: 1px solid rgba(255, 255, 255, 0.12);
    }

    .brand-mark {
      width: 44px;
      height: 44px;
      border-radius: 8px;
      display: grid;
      place-items: center;
      color: white;
      font-weight: 800;
      font-family: "Fira Code", "Microsoft YaHei", monospace;
      background:
        linear-gradient(135deg, rgba(45, 212, 191, 0.98), rgba(56, 189, 248, 0.95)),
        repeating-linear-gradient(90deg, transparent 0 7px, rgba(255, 255, 255, 0.22) 7px 8px);
      box-shadow: 0 0 24px rgba(45, 212, 191, 0.28);
    }

    .brand strong {
      display: block;
      font-size: 18px;
      line-height: 1.2;
    }

    .brand span {
      display: block;
      color: #9aa7ba;
      font-size: 12px;
      margin-top: 4px;
    }

    .nav {
      display: grid;
      gap: 8px;
    }

    .nav button {
      border: 0;
      border-radius: 8px;
      min-height: 40px;
      padding: 10px 12px 10px 14px;
      background: rgba(15, 23, 42, 0.18);
      color: #cbd5e1;
      text-align: left;
      position: relative;
      transition: background 0.18s ease, color 0.18s ease, border-color 0.18s ease, box-shadow 0.18s ease;
      border: 1px solid transparent;
    }

    .nav button.active,
    .nav button:hover {
      background: linear-gradient(90deg, rgba(56, 189, 248, 0.16), rgba(45, 212, 191, 0.09));
      border-color: rgba(56, 189, 248, 0.28);
      color: #ffffff;
      box-shadow: inset 0 0 18px rgba(56, 189, 248, 0.08);
    }

    .nav button.active::before {
      content: "";
      position: absolute;
      left: 0;
      top: 9px;
      bottom: 9px;
      width: 3px;
      border-radius: 999px;
      background: var(--teal);
      box-shadow: 0 0 14px rgba(45, 212, 191, 0.82);
    }

    .side-card {
      margin-top: auto;
      border: 1px solid rgba(56, 189, 248, 0.24);
      border-radius: 8px;
      padding: 14px;
      color: #cbd5e1;
      line-height: 1.6;
      font-size: 13px;
      background: rgba(15, 23, 42, 0.42);
      box-shadow: inset 0 0 28px rgba(56, 189, 248, 0.06);
    }

    .main {
      min-width: 0;
      max-width: 100%;
      overflow-x: hidden;
      padding: 24px 28px 36px;
    }

    .topbar {
      display: flex;
      align-items: flex-start;
      justify-content: space-between;
      gap: 18px;
      margin-bottom: 12px;
      background:
        linear-gradient(135deg, rgba(14, 24, 29, 0.92), rgba(5, 9, 13, 0.86));
      border: 1px solid var(--line);
      border-radius: 8px;
      box-shadow: var(--shadow-soft);
      padding: 18px;
      backdrop-filter: blur(16px);
      max-width: 100%;
    }

    h1 {
      margin: 0;
      font-size: 29px;
      letter-spacing: 0;
      color: #f8fafc;
      text-shadow: 0 0 16px rgba(56, 189, 248, 0.22);
    }

    .subtitle {
      margin-top: 8px;
      color: var(--muted);
      line-height: 1.6;
      max-width: 880px;
    }

    .actions {
      display: flex;
      gap: 10px;
      flex-wrap: wrap;
      justify-content: flex-end;
      max-width: 100%;
    }

    .btn {
      border: 1px solid var(--line);
      border-radius: 8px;
      min-height: 38px;
      padding: 8px 13px;
      background: rgba(15, 23, 42, 0.72);
      color: var(--ink);
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 7px;
      white-space: nowrap;
      box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.06);
      transition: transform 0.16s ease, box-shadow 0.16s ease, border-color 0.16s ease, background 0.16s ease;
    }

    .btn:hover {
      transform: translateY(-1px);
      border-color: var(--line-strong);
      background: rgba(15, 29, 52, 0.92);
      box-shadow: var(--glow-blue);
    }

    .btn:focus-visible,
    .nav button:focus-visible {
      outline: 3px solid rgba(56, 189, 248, 0.28);
      outline-offset: 2px;
    }

    .btn.primary {
      background: linear-gradient(135deg, #0f766e, var(--teal));
      border-color: var(--teal);
      color: #ecfeff;
      box-shadow: var(--glow-teal);
    }

    .btn.blue {
      background: linear-gradient(135deg, #1d4ed8, var(--blue));
      border-color: var(--blue);
      color: #eff6ff;
      box-shadow: var(--glow-blue);
    }

    .btn.danger {
      background: linear-gradient(135deg, #be123c, var(--red));
      border-color: var(--red);
      color: white;
    }

    .grid {
      display: grid;
      gap: 16px;
    }

    .metrics {
      grid-template-columns: repeat(5, minmax(140px, 1fr));
    }

    .metric,
    .card {
      background: var(--panel);
      border: 1px solid var(--line);
      border-radius: 8px;
      box-shadow: var(--shadow);
      backdrop-filter: blur(14px);
    }

    .metric {
      padding: 15px;
      border-top: 3px solid var(--blue);
      min-height: 112px;
      position: relative;
      overflow: hidden;
      background:
        linear-gradient(180deg, rgba(14, 24, 29, 0.92), rgba(5, 9, 13, 0.86));
    }

    .metric[role="button"],
    .context-item[role="button"],
    .rank-item[role="button"],
    .pipeline-item[role="button"],
    .matrix-item[role="button"],
    .action-item[role="button"] {
      cursor: pointer;
      outline: none;
    }

    .metric[role="button"]:hover,
    .context-item[role="button"]:hover,
    .rank-item[role="button"]:hover,
    .pipeline-item[role="button"]:hover,
    .matrix-item[role="button"]:hover,
    .action-item[role="button"]:hover {
      border-color: var(--line-strong);
      box-shadow: 0 16px 34px rgba(0, 0, 0, 0.3), var(--glow-blue);
    }

    .metric[role="button"]:focus-visible,
    .context-item[role="button"]:focus-visible,
    .rank-item[role="button"]:focus-visible,
    .pipeline-item[role="button"]:focus-visible,
    .matrix-item[role="button"]:focus-visible,
    .action-item[role="button"]:focus-visible {
      outline: 3px solid rgba(56, 189, 248, 0.28);
      outline-offset: 2px;
    }

    .metric::after {
      content: "";
      position: absolute;
      inset: auto 14px 12px auto;
      width: 42px;
      height: 42px;
      border: 1px solid rgba(56, 189, 248, 0.2);
      border-radius: 50%;
      box-shadow: inset 0 0 18px rgba(56, 189, 248, 0.12);
      opacity: 0.72;
    }

    .metric:nth-child(2) {
      border-top-color: var(--teal);
    }

    .metric:nth-child(3) {
      border-top-color: var(--red);
    }

    .metric:nth-child(4) {
      border-top-color: var(--green);
    }

    .metric:nth-child(5) {
      border-top-color: var(--amber);
    }

    .metric span {
      color: var(--muted);
      font-size: 13px;
    }

    .metric strong {
      display: block;
      margin-top: 8px;
      font-size: 27px;
      line-height: 1.1;
      color: #f8fafc;
      font-family: "Fira Code", "Microsoft YaHei", monospace;
    }

    .metric small {
      display: block;
      margin-top: 5px;
      color: var(--muted);
      font-size: 12px;
    }

    .layout {
      display: grid;
      grid-template-columns: minmax(340px, 1fr) minmax(420px, 1.25fr);
      gap: 16px;
      margin-top: 16px;
      align-items: start;
    }

    .layout.reverse {
      grid-template-columns: minmax(440px, 1.2fr) minmax(340px, 0.9fr);
    }

    .card {
      padding: 16px;
      min-width: 0;
      background:
        linear-gradient(180deg, rgba(14, 24, 29, 0.88), rgba(5, 9, 13, 0.84));
      transition: border-color 0.16s ease, box-shadow 0.16s ease, background 0.16s ease;
    }

    .card:hover {
      border-color: var(--line-strong);
      box-shadow: 0 18px 42px rgba(0, 0, 0, 0.36), var(--glow-blue);
    }

    .section-title {
      display: flex;
      align-items: flex-start;
      justify-content: space-between;
      gap: 14px;
      margin-bottom: 14px;
    }

    .section-title h2 {
      margin: 0;
      font-size: 18px;
      line-height: 1.25;
      color: #f8fafc;
    }

    .section-title p {
      margin: 4px 0 0;
      color: var(--muted);
      font-size: 13px;
      line-height: 1.5;
    }

    .device-list {
      display: grid;
      gap: 10px;
    }

    .device {
      border: 1px solid var(--line);
      border-radius: 8px;
      padding: 12px;
      background: rgba(7, 17, 31, 0.58);
      display: grid;
      grid-template-columns: 1fr auto;
      gap: 10px;
      cursor: pointer;
      outline: none;
      transition: background 0.16s ease, border-color 0.16s ease, transform 0.16s ease, box-shadow 0.16s ease;
    }

    .device:hover {
      transform: translateY(-1px);
      border-color: var(--line-strong);
      background: rgba(15, 29, 52, 0.86);
      box-shadow: var(--glow-blue);
    }

    .device:focus-visible {
      border-color: var(--blue);
      box-shadow: 0 0 0 3px rgba(29, 78, 216, 0.16);
    }

    .device.active {
      border-color: var(--teal);
      background: linear-gradient(90deg, rgba(45, 212, 191, 0.18), rgba(56, 189, 248, 0.08));
      box-shadow: inset 0 0 22px rgba(45, 212, 191, 0.08), var(--glow-teal);
    }

    .device h3 {
      margin: 0;
      font-size: 15px;
    }

    .device p {
      margin: 5px 0 0;
      color: var(--muted);
      font-size: 13px;
      line-height: 1.45;
    }

    .pill {
      border-radius: 999px;
      padding: 4px 9px;
      font-size: 12px;
      font-weight: 800;
      line-height: 1.3;
      white-space: nowrap;
      align-self: start;
      border: 1px solid currentColor;
      font-family: "Fira Code", "Microsoft YaHei", monospace;
    }

    .pill.green {
      background: var(--soft-green);
      color: var(--green);
    }

    .pill.amber {
      background: var(--soft-amber);
      color: var(--amber);
    }

    .pill.red {
      background: var(--soft-red);
      color: var(--red);
    }

    .pill.blue {
      background: var(--soft-blue);
      color: var(--blue);
    }

    .pill.violet {
      background: var(--soft-violet);
      color: var(--violet);
    }

    .chart {
      height: 280px;
      border: 1px solid var(--line);
      border-radius: 8px;
      background:
        linear-gradient(180deg, rgba(4, 12, 24, 0.96), rgba(8, 18, 33, 0.9));
      overflow: hidden;
      box-shadow: inset 0 0 32px rgba(56, 189, 248, 0.06);
    }

    canvas {
      width: 100%;
      height: 100%;
      display: block;
    }

    .sensor-grid {
      margin-top: 14px;
      display: grid;
      grid-template-columns: repeat(4, minmax(92px, 1fr));
      gap: 10px;
    }

    .sensor {
      border: 1px solid var(--line);
      border-radius: 8px;
      background: var(--panel-2);
      padding: 10px;
      box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.04);
    }

    .sensor span {
      color: var(--muted);
      font-size: 12px;
    }

    .sensor strong {
      display: block;
      margin-top: 4px;
      font-size: 18px;
      color: #f8fafc;
      font-family: "Fira Code", "Microsoft YaHei", monospace;
    }

    .sensor small {
      display: block;
      margin-top: 4px;
      color: var(--muted);
      font-size: 11px;
    }

    .detail-grid {
      display: grid;
      grid-template-columns: repeat(4, minmax(120px, 1fr));
      gap: 10px;
      margin-top: 14px;
    }

    .detail {
      border: 1px solid var(--line);
      border-radius: 8px;
      padding: 11px;
      background: var(--panel-2);
      box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.04);
    }

    .detail span {
      color: var(--muted);
      font-size: 12px;
    }

    .detail strong {
      display: block;
      margin-top: 5px;
      font-size: 16px;
      line-height: 1.35;
      color: #f8fafc;
    }

    .diagnosis {
      border-left: 4px solid var(--teal);
      background: linear-gradient(90deg, rgba(45, 212, 191, 0.13), rgba(15, 29, 52, 0.72));
      padding: 13px 14px;
      border-radius: 8px;
      line-height: 1.7;
      box-shadow: inset 0 0 24px rgba(45, 212, 191, 0.06);
    }

    .diagnosis strong {
      display: block;
      margin-bottom: 6px;
    }

    .evidence-list,
    .knowledge-list,
    .workflow {
      display: grid;
      gap: 10px;
    }

    .evidence {
      border: 1px solid var(--line);
      border-radius: 8px;
      padding: 11px 12px;
      display: grid;
      grid-template-columns: 1fr auto;
      gap: 8px;
      background: rgba(7, 17, 31, 0.58);
    }

    .evidence strong {
      display: block;
      font-size: 14px;
      margin-bottom: 4px;
    }

    .evidence span {
      color: var(--muted);
      font-size: 13px;
      line-height: 1.5;
    }

    .workflow-step {
      display: grid;
      grid-template-columns: 32px 1fr;
      gap: 10px;
      align-items: start;
    }

    .step-index {
      width: 30px;
      height: 30px;
      border-radius: 50%;
      background: var(--soft-blue);
      color: var(--blue);
      display: grid;
      place-items: center;
      font-weight: 800;
      font-size: 13px;
    }

    .workflow-step strong {
      display: block;
      font-size: 14px;
      margin-bottom: 3px;
    }

    .workflow-step span {
      color: var(--muted);
      font-size: 13px;
      line-height: 1.5;
    }

    .knowledge-item,
    .order,
    .formula {
      border: 1px solid var(--line);
      border-radius: 8px;
      padding: 12px;
      background: rgba(7, 17, 31, 0.58);
    }

    .knowledge-item strong,
    .order strong,
    .formula strong {
      display: block;
      margin-bottom: 6px;
    }

    .knowledge-item p,
    .order p,
    .formula p {
      margin: 0;
      color: var(--muted);
      line-height: 1.55;
      font-size: 13px;
    }

    .order-grid {
      display: grid;
      gap: 10px;
    }

    .order {
      display: grid;
      gap: 8px;
    }

    .order-row {
      display: flex;
      justify-content: space-between;
      gap: 10px;
      color: var(--muted);
      font-size: 13px;
    }

    .order-row b {
      color: var(--ink);
      text-align: right;
      font-family: "Fira Code", "Microsoft YaHei", monospace;
    }

    .table-wrap {
      border: 1px solid var(--line);
      border-radius: 8px;
      overflow: auto;
      background: rgba(7, 17, 31, 0.58);
      box-shadow: inset 0 0 24px rgba(56, 189, 248, 0.04);
    }

    table {
      width: 100%;
      min-width: 760px;
      border-collapse: collapse;
      font-size: 13px;
    }

    th,
    td {
      border-bottom: 1px solid var(--line);
      padding: 10px 11px;
      text-align: left;
      white-space: nowrap;
      color: #dbeafe;
    }

    th {
      background: rgba(15, 29, 52, 0.96);
      color: #dbeafe;
      font-weight: 800;
      position: sticky;
      top: 0;
      z-index: 1;
    }

    tbody tr:hover {
      background: rgba(56, 189, 248, 0.08);
    }

    tr:last-child td {
      border-bottom: 0;
    }

    .formula-list {
      display: grid;
      grid-template-columns: repeat(3, minmax(180px, 1fr));
      gap: 10px;
    }

    .view {
      display: none;
    }

    .view.active {
      display: block;
      animation: viewIn 0.18s ease-out;
    }

    @keyframes viewIn {
      from {
        opacity: 0;
        transform: translateY(4px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }

    .view-title {
      display: flex;
      align-items: flex-start;
      justify-content: space-between;
      gap: 16px;
      margin: 6px 0 16px;
    }

    .view-title h2 {
      margin: 0;
      font-size: 22px;
      color: #f8fafc;
      text-shadow: 0 0 14px rgba(45, 212, 191, 0.14);
    }

    .view-title p {
      margin: 6px 0 0;
      color: var(--muted);
      line-height: 1.55;
    }

    .dashboard-grid {
      display: grid;
      grid-template-columns: minmax(360px, 1.05fr) minmax(320px, 0.95fr);
      gap: 16px;
      margin-top: 16px;
    }

    .dashboard-wide-grid {
      display: grid;
      grid-template-columns: minmax(440px, 1.35fr) minmax(300px, 0.85fr);
      gap: 16px;
      margin-top: 16px;
      align-items: start;
    }

    .mini-btn {
      border: 1px solid var(--line);
      border-radius: 8px;
      background: rgba(15, 23, 42, 0.64);
      color: #dbeafe;
      min-height: 32px;
      padding: 6px 10px;
      white-space: nowrap;
      transition: border-color 0.16s ease, background 0.16s ease, box-shadow 0.16s ease;
    }

    .mini-btn:hover,
    .mini-btn:focus-visible {
      border-color: var(--line-strong);
      background: rgba(56, 189, 248, 0.12);
      box-shadow: var(--glow-blue);
      outline: none;
    }

    .matrix-grid {
      display: grid;
      grid-template-columns: repeat(3, minmax(160px, 1fr));
      gap: 10px;
    }

    .matrix-item,
    .action-item {
      border: 1px solid var(--line);
      border-radius: 8px;
      background: rgba(7, 17, 31, 0.58);
      padding: 12px;
      min-width: 0;
      transition: border-color 0.16s ease, box-shadow 0.16s ease, background 0.16s ease;
    }

    .matrix-item {
      display: grid;
      gap: 9px;
    }

    .matrix-head,
    .action-head {
      display: flex;
      align-items: flex-start;
      justify-content: space-between;
      gap: 10px;
    }

    .matrix-head strong,
    .action-head strong {
      color: #f8fafc;
      line-height: 1.35;
    }

    .matrix-item p,
    .action-item p {
      margin: 0;
      color: var(--muted);
      font-size: 13px;
      line-height: 1.5;
    }

    .matrix-meter {
      height: 8px;
      border: 1px solid rgba(148, 163, 184, 0.18);
      border-radius: 999px;
      overflow: hidden;
      background: rgba(148, 163, 184, 0.12);
    }

    .matrix-meter i {
      display: block;
      height: 100%;
      border-radius: inherit;
      background: linear-gradient(90deg, var(--teal), var(--blue));
      box-shadow: 0 0 14px rgba(56, 189, 248, 0.28);
    }

    .matrix-meter i.amber {
      background: linear-gradient(90deg, var(--amber), #fde68a);
      box-shadow: 0 0 14px rgba(245, 158, 11, 0.24);
    }

    .matrix-meter i.red {
      background: linear-gradient(90deg, #be123c, var(--red));
      box-shadow: 0 0 14px rgba(251, 113, 133, 0.26);
    }

    .action-queue {
      display: grid;
      gap: 10px;
    }

    .action-item {
      display: grid;
      gap: 8px;
    }

    .item-meta {
      display: flex;
      gap: 8px;
      flex-wrap: wrap;
      color: var(--muted);
      font-size: 12px;
      line-height: 1.4;
    }

    .item-meta b {
      color: #dbeafe;
      font-family: "Fira Code", "Microsoft YaHei", monospace;
    }

    .inline-action {
      color: var(--blue);
      font-size: 13px;
      font-weight: 800;
    }

    .rank-list,
    .profile-grid,
    .pipeline-grid,
    .quality-grid,
    .root-grid {
      display: grid;
      gap: 10px;
    }

    .rank-item,
    .profile-item,
    .pipeline-item,
    .quality-item,
    .root-item {
      border: 1px solid var(--line);
      border-radius: 8px;
      padding: 12px;
      background: rgba(7, 17, 31, 0.58);
    }

    .rank-item,
    .knowledge-item,
    .order,
    .quality-item,
    .root-item,
    .pipeline-item,
    .profile-item {
      position: relative;
      overflow: hidden;
    }

    .rank-item::before,
    .knowledge-item::before,
    .order::before,
    .quality-item::before,
    .root-item::before,
    .pipeline-item::before,
    .profile-item::before {
      content: "";
      position: absolute;
      left: 0;
      top: 0;
      bottom: 0;
      width: 3px;
      background: var(--teal);
      opacity: 0.75;
      box-shadow: 0 0 14px rgba(45, 212, 191, 0.6);
    }

    .rank-item {
      display: grid;
      grid-template-columns: 1fr auto;
      gap: 10px;
      align-items: start;
    }

    .rank-item strong,
    .profile-item strong,
    .pipeline-item strong,
    .quality-item strong,
    .root-item strong {
      display: block;
      margin-bottom: 5px;
      color: #f8fafc;
    }

    .rank-item p,
    .profile-item p,
    .pipeline-item p,
    .quality-item p,
    .root-item p {
      margin: 0;
      color: var(--muted);
      font-size: 13px;
      line-height: 1.55;
    }

    .compact-table table {
      min-width: 560px;
    }

    .pipeline-grid {
      grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
    }

    .quality-grid,
    .root-grid {
      grid-template-columns: repeat(2, minmax(180px, 1fr));
    }

    .context-strip {
      display: grid;
      grid-template-columns: minmax(190px, 1.4fr) repeat(4, minmax(130px, 1fr));
      gap: 10px;
      margin-bottom: 18px;
    }

    .context-item {
      border: 1px solid var(--line);
      border-radius: 8px;
      background: rgba(15, 29, 52, 0.72);
      box-shadow: var(--shadow-soft);
      padding: 11px 12px;
      min-width: 0;
      backdrop-filter: blur(12px);
    }

    .context-item span {
      display: block;
      color: var(--muted);
      font-size: 12px;
      margin-bottom: 5px;
    }

    .context-item strong {
      display: block;
      font-size: 15px;
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
      color: #f8fafc;
      font-family: "Fira Code", "Microsoft YaHei", monospace;
    }

    .footer-note {
      margin-top: 14px;
      color: var(--muted);
      font-size: 12px;
      line-height: 1.6;
    }

    @media (prefers-reduced-motion: reduce) {
      *,
      *::before,
      *::after {
        animation-duration: 0.001ms !important;
        animation-iteration-count: 1 !important;
        scroll-behavior: auto !important;
        transition-duration: 0.001ms !important;
      }
    }

    @media (max-width: 1180px) {
      .app {
        grid-template-columns: 1fr;
      }

      .sidebar {
        display: block;
        position: static;
        height: auto;
      }

      .brand {
        margin-bottom: 14px;
      }

      .nav {
        grid-template-columns: repeat(5, minmax(120px, 1fr));
      }

      .side-card {
        display: none;
      }

      .metrics {
        grid-template-columns: repeat(3, minmax(150px, 1fr));
      }

      .layout,
      .layout.reverse,
      .dashboard-grid,
      .dashboard-wide-grid,
      .context-strip {
        grid-template-columns: 1fr;
      }

      .pipeline-grid {
        grid-template-columns: repeat(2, minmax(150px, 1fr));
      }
    }

    @media (max-width: 760px) {
      .main {
        padding: 18px 14px 28px;
      }

      .topbar {
        display: block;
        width: min(100%, calc(100vw - 28px));
        min-width: 0;
        overflow: hidden;
      }

      .topbar .actions {
        margin-top: 14px;
      }

      .actions {
        display: grid;
        grid-template-columns: repeat(2, minmax(0, 1fr));
        justify-content: stretch;
        width: 100%;
        min-width: 0;
      }

      .btn {
        width: 100%;
        min-width: 0;
        padding-inline: 10px;
        white-space: normal;
        line-height: 1.35;
        overflow-wrap: anywhere;
      }

      .nav {
        grid-template-columns: 1fr 1fr;
      }

      .topbar {
        padding: 15px;
      }

      .metrics,
      .sensor-grid,
      .detail-grid,
      .formula-list,
      .matrix-grid,
      .quality-grid,
      .root-grid,
      .pipeline-grid {
        grid-template-columns: repeat(2, minmax(130px, 1fr));
      }

      h1 {
        font-size: 23px;
        overflow-wrap: anywhere;
      }

      .subtitle {
        overflow-wrap: anywhere;
      }

      .view-title {
        display: grid;
      }

      .section-title {
        display: grid;
      }

      .mini-btn {
        width: 100%;
      }
    }

    @media (max-width: 520px) {
      .actions {
        grid-template-columns: 1fr;
      }

      .metrics,
      .sensor-grid,
      .detail-grid,
      .formula-list,
      .matrix-grid,
      .quality-grid,
      .root-grid,
      .pipeline-grid {
        grid-template-columns: 1fr;
      }
    }
  </style>
</head>
<body>
  <div class="app">
    <aside class="sidebar">
      <div class="brand">
        <div class="brand-mark">AI</div>
        <div>
          <strong>智维工场</strong>
          <span>多智能体预测性维护平台</span>
        </div>
      </div>
      <nav class="nav" aria-label="主导航">
        <button class="active" data-view-target="dashboard">驾驶舱</button>
        <button data-view-target="profile">设备画像</button>
        <button data-view-target="diagnosis">AI诊断</button>
        <button data-view-target="orders">工单闭环</button>
        <button data-view-target="data">数据处理</button>
      </nav>
      <div class="side-card">
        单文件离线原型。健康分、风险等级、RUL、知识库命中和工单字段均由样例数据实时计算，便于现场复现和答辩说明。
      </div>
    </aside>

    <main class="main">
      <header class="topbar">
        <div>
          <h1 id="pageTitle">工业设备AI预测性维护驾驶舱</h1>
          <div class="subtitle" id="pageSubtitle">
            面向新工科实验室与中小制造产线，整合设备时序数据、阈值基线、知识库检索和多智能体工作流，形成从异常发现到维修复盘的闭环应用。
          </div>
        </div>
        <div class="actions">
          <button class="btn" id="baselineBtn">恢复基线数据</button>
          <button class="btn danger" id="injectBtn">注入高风险样本</button>
          <button class="btn primary" id="diagnoseBtn">运行AI诊断</button>
          <button class="btn blue" id="orderBtn">生成维护工单</button>
        </div>
      </header>

      <section class="context-strip" aria-label="当前设备状态">
        <div class="context-item" role="button" tabindex="0" data-dashboard-action="selected-profile">
          <span>当前设备</span>
          <strong id="contextAsset">-</strong>
        </div>
        <div class="context-item" role="button" tabindex="0" data-dashboard-action="selected-profile">
          <span>风险等级</span>
          <strong id="contextRisk">-</strong>
        </div>
        <div class="context-item" role="button" tabindex="0" data-dashboard-action="selected-profile">
          <span>健康分</span>
          <strong id="contextHealth">-</strong>
        </div>
        <div class="context-item" role="button" tabindex="0" data-dashboard-action="selected-profile">
          <span>剩余寿命</span>
          <strong id="contextRul">-</strong>
        </div>
        <div class="context-item" role="button" tabindex="0" data-dashboard-action="data">
          <span>最新采样</span>
          <strong id="contextSample">-</strong>
        </div>
      </section>

      <section class="view active" data-view="dashboard">
        <div class="view-title">
          <div>
            <h2>驾驶舱总览</h2>
            <p>集中展示设备健康、数据质量、风险态势和待处理任务，作为现场演示的入口。</p>
          </div>
          <span class="pill blue">全局态势</span>
        </div>

        <div class="grid metrics" aria-label="核心指标">
          <div class="metric" role="button" tabindex="0" data-dashboard-action="profile">
            <span>接入设备</span>
            <strong id="metricDevices">0</strong>
            <small>点击查看设备健康矩阵</small>
          </div>
          <div class="metric" role="button" tabindex="0" data-dashboard-action="selected-profile">
            <span>平均健康分</span>
            <strong id="metricScore">0</strong>
            <small>点击查看当前设备画像</small>
          </div>
          <div class="metric" role="button" tabindex="0" data-dashboard-action="worst-profile">
            <span>高风险设备</span>
            <strong id="metricRisk">0</strong>
            <small>点击定位风险最高设备</small>
          </div>
          <div class="metric" role="button" tabindex="0" data-dashboard-action="data">
            <span>数据质量</span>
            <strong id="metricQuality">0%</strong>
            <small>点击查看数据处理链路</small>
          </div>
          <div class="metric" role="button" tabindex="0" data-dashboard-action="orders">
            <span>待处理工单</span>
            <strong id="metricOrders">0</strong>
            <small>点击查看工单闭环</small>
          </div>
        </div>

        <div class="dashboard-wide-grid">
          <div class="card">
            <div class="section-title">
              <div>
                <h2>设备健康矩阵</h2>
                <p>按风险等级、健康分和RUL集中浏览，点击设备进入画像详情。</p>
              </div>
              <button class="mini-btn" data-dashboard-action="profile">查看全部</button>
            </div>
            <div class="matrix-grid" id="healthMatrix"></div>
          </div>

          <div class="card">
            <div class="section-title">
              <div>
                <h2>现场处置队列</h2>
                <p>把风险排序转化为可执行动作，支持一键进入诊断或工单。</p>
              </div>
              <button class="mini-btn" data-dashboard-action="diagnosis">运行诊断</button>
            </div>
            <div class="action-queue" id="actionQueue"></div>
          </div>
        </div>

        <div class="dashboard-grid">
          <div class="card">
            <div class="section-title">
              <div>
                <h2>风险排行</h2>
                <p>按健康分、异常指数和剩余寿命综合排序。</p>
              </div>
              <button class="mini-btn" data-dashboard-action="worst-profile">定位最高风险</button>
            </div>
            <div class="rank-list" id="riskRankList"></div>
          </div>

          <div class="card">
            <div class="section-title">
              <div>
                <h2>系统能力</h2>
                <p>覆盖设备画像、诊断决策、维护执行和数据处理。</p>
              </div>
              <button class="mini-btn" data-dashboard-action="data">查看链路</button>
            </div>
            <div class="pipeline-grid" id="systemCapabilityList"></div>
          </div>
        </div>
      </section>

      <section class="view" data-view="profile">
        <div class="view-title">
          <div>
            <h2>设备画像</h2>
            <p>沉淀设备档案、责任归属、维护周期、传感器阈值和健康趋势，支撑后续诊断与派单。</p>
          </div>
          <span class="pill blue" id="matrixMode">实时评估</span>
        </div>

        <section class="layout">
          <div class="card">
            <div class="section-title">
              <div>
                <h2>设备健康矩阵</h2>
                <p>选择设备后，右侧实时刷新健康分、风险证据、RUL和诊断建议。</p>
              </div>
            </div>
            <div class="device-list" id="deviceList"></div>
          </div>

          <div class="card">
            <div class="section-title">
              <div>
                <h2 id="selectedTitle">设备详情</h2>
                <p id="selectedMeta">设备类型、位置与维护状态</p>
              </div>
              <span class="pill green" id="selectedRisk">稳定</span>
            </div>
            <div class="chart">
              <canvas id="healthCanvas" width="920" height="330" aria-label="健康分趋势图"></canvas>
            </div>
            <div class="sensor-grid" id="sensorGrid"></div>
            <div class="detail-grid" id="detailGrid"></div>
            <div class="section-title" style="margin-top:16px;">
              <div>
                <h2>画像档案</h2>
                <p>设备、维护和寿命数据统一挂接到当前资产。</p>
              </div>
            </div>
            <div class="profile-grid" id="profileGrid"></div>
            <div class="table-wrap compact-table" style="margin-top:14px;">
              <table>
                <thead>
                  <tr>
                    <th>传感器</th>
                    <th>正常下限</th>
                    <th>预警阈值</th>
                    <th>危险阈值</th>
                    <th>物理上限</th>
                  </tr>
                </thead>
                <tbody id="thresholdRows"></tbody>
              </table>
            </div>
          </div>
        </section>
      </section>

      <section class="view" data-view="diagnosis">
        <div class="view-title">
          <div>
            <h2>AI诊断</h2>
            <p>将阈值证据、趋势斜率、知识库命中、根因概率和智能体工作流组合成结构化诊断报告。</p>
          </div>
          <span class="pill violet" id="confidencePill">置信度 0%</span>
        </div>

        <section class="layout reverse">
          <div class="card">
            <div class="section-title">
              <div>
                <h2>AI诊断中心</h2>
                <p>诊断结论由阈值证据、趋势斜率、知识库案例和工单策略共同生成。</p>
              </div>
            </div>
            <div class="diagnosis" id="diagnosisBox">
              <strong>诊断结论</strong>
              点击“运行AI诊断”后生成结构化诊断报告。
            </div>
            <div class="detail-grid" id="riskSummary"></div>
            <div class="section-title" style="margin-top:16px;">
              <div>
                <h2>异常证据</h2>
                <p>每条证据均来自传感器最新值、阈值基线或趋势变化。</p>
              </div>
            </div>
            <div class="evidence-list" id="evidenceList"></div>
          </div>

          <div class="card">
            <div class="section-title">
              <div>
                <h2>智能体工作流</h2>
                <p>监测、检索、诊断、工单和复盘的执行链路。</p>
              </div>
            </div>
            <div class="workflow" id="workflowList"></div>
            <div class="section-title" style="margin-top:16px;">
              <div>
                <h2>根因概率</h2>
                <p>根据异常证据和知识库标签估算可解释根因。</p>
              </div>
            </div>
            <div class="root-grid" id="rootCauseList"></div>
          </div>
        </section>

        <section class="layout">
          <div class="card">
            <div class="section-title">
              <div>
                <h2>知识库命中</h2>
                <p>按设备类型、异常标签和安全规范计算匹配分。</p>
              </div>
            </div>
            <div class="knowledge-list" id="knowledgeList"></div>
          </div>
          <div class="card">
            <div class="section-title">
              <div>
                <h2>诊断输出规范</h2>
                <p>保证AI结论可解释、可执行、可追溯。</p>
              </div>
            </div>
            <div class="pipeline-grid">
              <div class="pipeline-item"><strong>输入</strong><p>设备画像、最新采样、阈值、历史趋势。</p></div>
              <div class="pipeline-item"><strong>证据</strong><p>预警项、危险项、耦合异常和趋势斜率。</p></div>
              <div class="pipeline-item"><strong>结论</strong><p>风险等级、RUL、置信度和推荐操作。</p></div>
              <div class="pipeline-item"><strong>约束</strong><p>不编造数据，必须引用触发指标和知识条目。</p></div>
            </div>
          </div>
        </section>
      </section>

      <section class="view" data-view="orders">
        <div class="view-title">
          <div>
            <h2>工单闭环</h2>
            <p>把AI诊断转为可执行任务，保留审核、执行、验收、复盘和知识库回写字段。</p>
          </div>
          <button class="btn" id="closeOrderBtn">完成最高优先级工单</button>
        </div>

        <section class="layout">
          <div class="card">
            <div class="section-title">
              <div>
                <h2>工单列表</h2>
                <p>AI建议生成后，保留人工审核、执行和验收字段。</p>
              </div>
            </div>
            <div class="order-grid" id="orderList"></div>
          </div>

          <div class="card">
            <div class="section-title">
              <div>
                <h2>闭环统计</h2>
                <p>从风险识别到维修复盘的过程质量。</p>
              </div>
            </div>
            <div class="quality-grid" id="orderStats"></div>
          </div>
        </section>
      </section>

      <section class="view" data-view="data">
        <div class="view-title">
          <div>
            <h2>数据处理</h2>
            <p>展示采样数据、清洗规则、质量校验、异常指数和模型计算口径，说明数据严谨性。</p>
          </div>
          <span class="pill blue">可追溯计算</span>
        </div>

        <section class="layout reverse">
          <div class="card">
            <div class="section-title">
              <div>
                <h2>样例时序数据</h2>
                <p>展示最近8个采样点，采样间隔10分钟，异常指数由归一化偏离度计算。</p>
              </div>
            </div>
            <div class="table-wrap">
              <table>
                <thead>
                  <tr>
                    <th>时间</th>
                    <th>温度 ℃</th>
                    <th>振动 RMS</th>
                    <th>电流 A</th>
                    <th>负载率</th>
                    <th>健康分</th>
                    <th>异常指数</th>
                    <th>判定</th>
                  </tr>
                </thead>
                <tbody id="sampleRows"></tbody>
              </table>
            </div>
          </div>

          <div class="card">
            <div class="section-title">
              <div>
                <h2>数据质量与处理链路</h2>
                <p>从采集、校验、特征计算到诊断输入的完整过程。</p>
              </div>
            </div>
            <div class="quality-grid" id="qualityList"></div>
            <div class="pipeline-grid" id="pipelineList" style="margin-top:14px;"></div>
          </div>
        </section>

        <section class="layout">
          <div class="card">
            <div class="section-title">
              <div>
                <h2>计算口径</h2>
                <p>答辩时可说明数据严谨性，避免只做界面展示。</p>
              </div>
            </div>
            <div class="formula-list">
              <div class="formula">
                <strong>健康分</strong>
                <p>100 - 温度惩罚30% - 振动惩罚35% - 电流惩罚20% - 负载惩罚15% - 趋势惩罚。</p>
              </div>
              <div class="formula">
                <strong>RUL估计</strong>
                <p>按设备基准寿命、风险等级、趋势下降斜率和危险阈值触发情况估算剩余可运行小时。</p>
              </div>
              <div class="formula">
                <strong>数据质量</strong>
                <p>检查缺失值、物理越界值和采样间隔偏差，输出可追溯质量分。</p>
              </div>
            </div>
          </div>

          <div class="card">
            <div class="section-title">
              <div>
                <h2>风险构成</h2>
                <p>最新采样值与危险阈值的比例，辅助解释异常来源。</p>
              </div>
            </div>
            <div class="chart">
              <canvas id="riskCanvas" width="920" height="330" aria-label="风险构成图"></canvas>
            </div>
          </div>
        </section>
      </section>

      <div class="footer-note">
        原型文件无需服务器即可打开。实际参赛落地时，可将本地样例数据替换为设备网关、CSV导入或AI无代码平台数据表，并将知识库模块连接向量检索服务。
      </div>
    </main>
  </div>

  <script>
    const baselineAssets = [
      {
        id: "CNC-01",
        name: "CNC-01 数控主轴",
        type: "数控加工中心",
        location: "智能制造实训区A",
        owner: "实验室管理员",
        baseLifeHours: 520,
        maintenanceCycle: 240,
        lastMaintenanceHours: 186,
        thresholds: {
          temperature: { warn: 68, danger: 78, min: 10, max: 95, unit: "℃" },
          vibration: { warn: 3.8, danger: 5.0, min: 0, max: 8, unit: "RMS" },
          current: { warn: 18.5, danger: 22.0, min: 0, max: 30, unit: "A" },
          load: { warn: 0.82, danger: 0.92, min: 0, max: 1, unit: "" }
        },
        samples: [
          ["09:00", 55.8, 2.2, 14.8, 0.61],
          ["09:10", 57.1, 2.4, 15.2, 0.64],
          ["09:20", 58.6, 2.6, 15.5, 0.66],
          ["09:30", 60.2, 2.8, 15.9, 0.68],
          ["09:40", 61.7, 3.0, 16.3, 0.70],
          ["09:50", 63.4, 3.3, 16.7, 0.72],
          ["10:00", 64.8, 3.5, 17.2, 0.74],
          ["10:10", 66.1, 3.7, 17.5, 0.76]
        ]
      },
      {
        id: "RB-02",
        name: "RB-02 六轴机器人",
        type: "工业机器人",
        location: "柔性制造单元",
        owner: "机器人课程组",
        baseLifeHours: 740,
        maintenanceCycle: 360,
        lastMaintenanceHours: 92,
        thresholds: {
          temperature: { warn: 62, danger: 72, min: 5, max: 90, unit: "℃" },
          vibration: { warn: 3.0, danger: 4.4, min: 0, max: 7, unit: "RMS" },
          current: { warn: 12.0, danger: 15.5, min: 0, max: 24, unit: "A" },
          load: { warn: 0.78, danger: 0.90, min: 0, max: 1, unit: "" }
        },
        samples: [
          ["09:00", 44.1, 1.4, 8.4, 0.42],
          ["09:10", 45.0, 1.5, 8.6, 0.43],
          ["09:20", 45.5, 1.5, 8.9, 0.45],
          ["09:30", 46.2, 1.6, 9.1, 0.46],
          ["09:40", 47.0, 1.7, 9.2, 0.47],
          ["09:50", 47.4, 1.7, 9.3, 0.49],
          ["10:00", 47.8, 1.8, 9.5, 0.50],
          ["10:10", 48.1, 1.8, 9.6, 0.51]
        ]
      },
      {
        id: "ACP-03",
        name: "ACP-03 空压机",
        type: "动力设备",
        location: "设备动力间",
        owner: "设备保障组",
        baseLifeHours: 420,
        maintenanceCycle: 180,
        lastMaintenanceHours: 174,
        thresholds: {
          temperature: { warn: 72, danger: 82, min: 10, max: 105, unit: "℃" },
          vibration: { warn: 4.2, danger: 5.6, min: 0, max: 9, unit: "RMS" },
          current: { warn: 20.0, danger: 24.0, min: 0, max: 34, unit: "A" },
          load: { warn: 0.84, danger: 0.94, min: 0, max: 1, unit: "" }
        },
        samples: [
          ["09:00", 63.6, 3.1, 17.2, 0.70],
          ["09:10", 65.8, 3.4, 17.8, 0.73],
          ["09:20", 68.4, 3.7, 18.4, 0.76],
          ["09:30", 70.9, 4.0, 19.1, 0.78],
          ["09:40", 73.2, 4.3, 19.9, 0.81],
          ["09:50", 75.7, 4.7, 20.8, 0.84],
          ["10:00", 77.9, 5.0, 21.6, 0.86],
          ["10:10", 79.8, 5.3, 22.4, 0.88]
        ]
      },
      {
        id: "AGV-04",
        name: "AGV-04 移动小车",
        type: "移动机器人",
        location: "物流实训线",
        owner: "物流工程课程组",
        baseLifeHours: 620,
        maintenanceCycle: 300,
        lastMaintenanceHours: 120,
        thresholds: {
          temperature: { warn: 58, danger: 68, min: 5, max: 85, unit: "℃" },
          vibration: { warn: 3.2, danger: 4.5, min: 0, max: 7, unit: "RMS" },
          current: { warn: 10.5, danger: 13.5, min: 0, max: 20, unit: "A" },
          load: { warn: 0.75, danger: 0.88, min: 0, max: 1, unit: "" }
        },
        samples: [
          ["09:00", 39.8, 1.8, 6.8, 0.43],
          ["09:10", 40.2, 1.9, 7.0, 0.45],
          ["09:20", 40.6, 1.9, 7.1, 0.46],
          ["09:30", 41.1, 2.0, 7.2, 0.47],
          ["09:40", 41.7, 2.0, 7.4, 0.49],
          ["09:50", 42.0, 2.1, 7.5, 0.50],
          ["10:00", 42.3, 2.1, 7.6, 0.50],
          ["10:10", 42.7, 2.2, 7.8, 0.52]
        ]
      },
      {
        id: "PRN-05",
        name: "PRN-05 工业3D打印机",
        type: "增材制造设备",
        location: "创新制造区",
        owner: "材料成型课程组",
        baseLifeHours: 480,
        maintenanceCycle: 220,
        lastMaintenanceHours: 161,
        thresholds: {
          temperature: { warn: 70, danger: 82, min: 10, max: 110, unit: "℃" },
          vibration: { warn: 2.8, danger: 4.1, min: 0, max: 6, unit: "RMS" },
          current: { warn: 12.8, danger: 16.0, min: 0, max: 24, unit: "A" },
          load: { warn: 0.80, danger: 0.92, min: 0, max: 1, unit: "" }
        },
        samples: [
          ["09:00", 58.0, 1.7, 9.1, 0.48],
          ["09:10", 59.6, 1.8, 9.5, 0.51],
          ["09:20", 61.4, 2.0, 9.8, 0.54],
          ["09:30", 63.8, 2.2, 10.4, 0.58],
          ["09:40", 66.1, 2.4, 10.9, 0.61],
          ["09:50", 68.2, 2.6, 11.3, 0.64],
          ["10:00", 70.1, 2.8, 11.8, 0.67],
          ["10:10", 71.8, 3.0, 12.1, 0.69]
        ]
      },
      {
        id: "CV-06",
        name: "CV-06 自动传送线",
        type: "自动化产线",
        location: "装配实训线",
        owner: "自动化课程组",
        baseLifeHours: 660,
        maintenanceCycle: 320,
        lastMaintenanceHours: 142,
        thresholds: {
          temperature: { warn: 60, danger: 72, min: 5, max: 90, unit: "℃" },
          vibration: { warn: 3.4, danger: 4.8, min: 0, max: 7, unit: "RMS" },
          current: { warn: 13.5, danger: 17.0, min: 0, max: 26, unit: "A" },
          load: { warn: 0.82, danger: 0.93, min: 0, max: 1, unit: "" }
        },
        samples: [
          ["09:00", 43.8, 2.0, 9.8, 0.51],
          ["09:10", 44.4, 2.1, 9.9, 0.52],
          ["09:20", 45.0, 2.1, 10.0, 0.53],
          ["09:30", 45.6, 2.2, 10.2, 0.55],
          ["09:40", 46.0, 2.2, 10.3, 0.55],
          ["09:50", 46.4, 2.3, 10.5, 0.56],
          ["10:00", 46.8, 2.3, 10.6, 0.57],
          ["10:10", 47.1, 2.4, 10.8, 0.58]
        ]
      }
    ];

    const knowledgeBase = [
      {
        id: "KB-001",
        title: "主轴轴承磨损与润滑不足",
        tags: ["数控加工中心", "vibration", "temperature", "bearing"],
        action: "检查主轴轴承间隙、润滑脂状态和同轴度，必要时安排更换轴承组件。",
        safety: "停机后执行断电挂牌，主轴完全停止后再拆检。"
      },
      {
        id: "KB-002",
        title: "空压机滤芯堵塞与散热异常",
        tags: ["动力设备", "temperature", "current", "load"],
        action: "检查进气滤芯、散热通道、润滑油液位和压力泄漏点。",
        safety: "释放残余压力后再拆卸滤芯或管路。"
      },
      {
        id: "KB-003",
        title: "机器人关节减速器温升",
        tags: ["工业机器人", "temperature", "current", "joint"],
        action: "检查关节润滑状态、负载曲线、重复定位误差和减速器异响。",
        safety: "进入机器人工作半径前必须切换示教低速模式。"
      },
      {
        id: "KB-004",
        title: "AGV驱动轮阻力与电池负载异常",
        tags: ["移动机器人", "current", "load", "vibration"],
        action: "检查驱动轮磨损、地面阻力、载荷分布和电池输出稳定性。",
        safety: "检修前启用驻车制动，确认路径区域无人。"
      },
      {
        id: "KB-005",
        title: "3D打印喷头温控波动",
        tags: ["增材制造设备", "temperature", "current"],
        action: "检查喷头温控模块、热敏电阻、加热棒和材料进给阻力。",
        safety: "高温喷头冷却至安全温度后再进行拆装。"
      },
      {
        id: "KB-006",
        title: "传送线轴承与皮带偏载",
        tags: ["自动化产线", "vibration", "load", "bearing"],
        action: "检查皮带张紧度、托辊轴承、载荷分布和电机固定状态。",
        safety: "维修前锁定急停并挂检修标识。"
      }
    ];

    const metricMeta = {
      temperature: { label: "温度", weight: 0.30, decimals: 1 },
      vibration: { label: "振动RMS", weight: 0.35, decimals: 1 },
      current: { label: "工作电流", weight: 0.20, decimals: 1 },
      load: { label: "负载率", weight: 0.15, decimals: 2 }
    };

    let assets = cloneAssets(baselineAssets);
    let selectedIndex = 0;
    let orders = [
      {
        id: "WO-20260610-001",
        assetId: "ACP-03",
        title: "空压机高温趋势复核",
        priority: "P2 优先",
        status: "待执行",
        parts: "滤芯、润滑油、密封圈",
        acceptance: "温度回落至72℃以下，电流低于20A"
      }
    ];
    let lastDiagnosis = null;
    let currentView = "dashboard";

    const viewConfig = {
      dashboard: {
        title: "工业设备AI预测性维护驾驶舱",
        subtitle: "面向新工科实验室与中小制造产线，整合设备时序数据、阈值基线、知识库检索和多智能体工作流，形成从异常发现到维修复盘的闭环应用。"
      },
      profile: {
        title: "设备画像",
        subtitle: "为每台设备建立档案、阈值、传感器、维护周期和健康趋势画像，支撑精准诊断。"
      },
      diagnosis: {
        title: "AI诊断",
        subtitle: "通过异常证据、趋势斜率、知识库命中和根因概率，输出可解释、可执行的诊断建议。"
      },
      orders: {
        title: "工单闭环",
        subtitle: "将AI诊断结果转化为审核、执行、验收和复盘任务，形成运维管理闭环。"
      },
      data: {
        title: "数据处理",
        subtitle: "展示采样数据、质量校验、异常指数、健康分和RUL计算口径，保证数据严谨可追溯。"
      }
    };

    const $ = id => document.getElementById(id);

    function cloneAssets(source) {
      return JSON.parse(JSON.stringify(source));
    }

    function clamp(value, min, max) {
      return Math.max(min, Math.min(max, value));
    }

    function latestSample(asset) {
      const row = asset.samples[asset.samples.length - 1];
      return {
        time: row[0],
        temperature: row[1],
        vibration: row[2],
        current: row[3],
        load: row[4]
      };
    }

    function metricPenalty(value, threshold, key) {
      const warn = threshold.warn;
      const danger = threshold.danger;
      const ratio = clamp((value - warn) / (danger - warn), 0, 1.35);
      return ratio * 100 * metricMeta[key].weight;
    }

    function slope(values) {
      if (values.length < 2) return 0;
      const n = values.length;
      const xMean = (n - 1) / 2;
      const yMean = values.reduce((sum, item) => sum + item, 0) / n;
      let numerator = 0;
      let denominator = 0;
      values.forEach((value, index) => {
        numerator += (index - xMean) * (value - yMean);
        denominator += Math.pow(index - xMean, 2);
      });
      return denominator === 0 ? 0 : numerator / denominator;
    }

    function sampleHealth(asset, sample) {
      const values = {
        temperature: sample[1],
        vibration: sample[2],
        current: sample[3],
        load: sample[4]
      };
      let penalty = 0;
      Object.keys(metricMeta).forEach(key => {
        penalty += metricPenalty(values[key], asset.thresholds[key], key);
      });
      return Math.round(clamp(100 - penalty, 35, 99));
    }

    function assetAnalysis(asset) {
      const latest = latestSample(asset);
      const healthSeries = asset.samples.map(sample => sampleHealth(asset, sample));
      const health = healthSeries[healthSeries.length - 1];
      const healthSlope = slope(healthSeries);
      const tempSlope = slope(asset.samples.map(row => row[1]));
      const vibrationSlope = slope(asset.samples.map(row => row[2]));
      const evidence = [];
      let dangerCount = 0;
      let warnCount = 0;
      let weightedPenalty = 0;

      Object.keys(metricMeta).forEach(key => {
        const value = latest[key];
        const threshold = asset.thresholds[key];
        const penalty = metricPenalty(value, threshold, key);
        weightedPenalty += penalty;
        if (value >= threshold.danger) {
          dangerCount += 1;
          evidence.push({
            level: "danger",
            key,
            title: `${metricMeta[key].label}触发危险阈值`,
            detail: `${formatMetric(key, value, threshold)}，危险阈值为${formatMetric(key, threshold.danger, threshold)}。`
          });
        } else if (value >= threshold.warn) {
          warnCount += 1;
          evidence.push({
            level: "warn",
            key,
            title: `${metricMeta[key].label}触发预警阈值`,
            detail: `${formatMetric(key, value, threshold)}，预警阈值为${formatMetric(key, threshold.warn, threshold)}。`
          });
        }
      });

      if (healthSlope <= -3) {
        evidence.push({
          level: "warn",
          key: "trend",
          title: "健康分连续下降",
          detail: `近8次采样健康分斜率为${healthSlope.toFixed(2)}分/采样点，存在加速劣化趋势。`
        });
      }

      if (tempSlope >= 1.8 && vibrationSlope >= 0.25) {
        evidence.push({
          level: "danger",
          key: "coupling",
          title: "温升与振动耦合上升",
          detail: `温度斜率${tempSlope.toFixed(2)}℃/采样点，振动斜率${vibrationSlope.toFixed(2)}RMS/采样点，符合机械摩擦或轴承劣化特征。`
        });
      }

      const risk = dangerCount > 0 || health < 70 ? "red" : warnCount > 0 || health < 82 ? "amber" : "green";
      const riskText = risk === "red" ? "高风险" : risk === "amber" ? "中风险" : "稳定";
      const anomalyIndex = clamp(Math.round(weightedPenalty + Math.abs(Math.min(healthSlope, 0)) * 4), 0, 100);
      const rul = estimateRul(asset, health, risk, healthSlope, dangerCount);
      const confidence = estimateConfidence(evidence, asset);
      const matches = matchKnowledge(asset, evidence);
      const quality = dataQuality(asset);

      return {
        latest,
        health,
        healthSeries,
        healthSlope,
        tempSlope,
        vibrationSlope,
        evidence,
        risk,
        riskText,
        anomalyIndex,
        rul,
        confidence,
        matches,
        quality
      };
    }

    function estimateRul(asset, health, risk, healthSlope, dangerCount) {
      const cycleRemain = Math.max(asset.maintenanceCycle - asset.lastMaintenanceHours, 0);
      const riskFactor = risk === "red" ? 0.32 : risk === "amber" ? 0.62 : 0.92;
      const trendFactor = clamp(1 + healthSlope / 18, 0.35, 1);
      const dangerFactor = Math.max(0.45, 1 - dangerCount * 0.16);
      const scoreFactor = clamp(health / 100, 0.35, 0.98);
      return Math.round(Math.min(asset.baseLifeHours, cycleRemain + asset.baseLifeHours * riskFactor * trendFactor * scoreFactor * dangerFactor * 0.45));
    }

    function estimateConfidence(evidence, asset) {
      const sampleScore = asset.samples.length >= 8 ? 20 : asset.samples.length * 2;
      const evidenceScore = Math.min(evidence.length * 12, 45);
      const qualityScore = Math.round(dataQuality(asset).score * 0.25);
      const crossScore = evidence.some(item => item.key === "coupling") ? 10 : 0;
      return clamp(sampleScore + evidenceScore + qualityScore + crossScore, 48, 96);
    }

    function dataQuality(asset) {
      let total = 0;
      let invalid = 0;
      let missing = 0;
      asset.samples.forEach(sample => {
        ["temperature", "vibration", "current", "load"].forEach((key, index) => {
          total += 1;
          const value = sample[index + 1];
          const rule = asset.thresholds[key];
          if (value === null || value === undefined || Number.isNaN(value)) {
            missing += 1;
            invalid += 1;
          } else if (value < rule.min || value > rule.max) {
            invalid += 1;
          }
        });
      });
      const intervalScore = asset.samples.length === 8 ? 100 : 85;
      const validScore = total === 0 ? 0 : Math.round((1 - invalid / total) * 100);
      const score = Math.round(validScore * 0.8 + intervalScore * 0.2);
      return { score, invalid, missing, total };
    }

    function matchKnowledge(asset, evidence) {
      const evidenceTags = evidence.map(item => item.key);
      return knowledgeBase
        .map(item => {
          let score = item.tags.includes(asset.type) ? 46 : 0;
          evidenceTags.forEach(tag => {
            if (item.tags.includes(tag)) score += 18;
          });
          if (evidenceTags.includes("coupling") && item.tags.includes("bearing")) score += 12;
          return { ...item, score: Math.min(score, 98) };
        })
        .filter(item => item.score >= 34)
        .sort((a, b) => b.score - a.score)
        .slice(0, 3);
    }

    function formatMetric(key, value, threshold) {
      if (key === "load") return `${Math.round(value * 100)}%`;
      return `${value.toFixed(metricMeta[key].decimals)}${threshold.unit}`;
    }

    function riskBadge(level) {
      if (level === "danger" || level === "red") return "red";
      if (level === "warn" || level === "amber") return "amber";
      return "green";
    }

    function priorityFromAnalysis(analysis) {
      if (analysis.risk === "red" || analysis.rul < 72) return "P1 紧急";
      if (analysis.risk === "amber" || analysis.rul < 180) return "P2 优先";
      return "P3 常规";
    }

    function recommendation(asset, analysis) {
      const top = analysis.matches[0];
      if (analysis.risk === "red") {
        return `建议在${Math.min(24, analysis.rul)}小时内安排停机窗口，执行${top ? top.action : "关键部件专项检查"}。`;
      }
      if (analysis.risk === "amber") {
        return `建议在下一维护窗口复核异常指标，重点执行${top ? top.action : "润滑、紧固和传感器校验"}。`;
      }
      return "设备运行稳定，建议保持日常巡检，并将当前数据作为健康基线样本。";
    }

    function switchView(view) {
      currentView = viewConfig[view] ? view : "dashboard";
      document.querySelectorAll("[data-view]").forEach(panel => {
        panel.classList.toggle("active", panel.dataset.view === currentView);
      });
      document.querySelectorAll("[data-view-target]").forEach(button => {
        button.classList.toggle("active", button.dataset.viewTarget === currentView);
      });
      renderPageChrome();
    }

    function renderPageChrome() {
      const config = viewConfig[currentView];
      $("pageTitle").textContent = config.title;
      $("pageSubtitle").textContent = config.subtitle;
    }

    function renderContextStrip() {
      const asset = assets[selectedIndex];
      const analysis = assetAnalysis(asset);
      $("contextAsset").textContent = asset.name;
      $("contextRisk").textContent = analysis.riskText;
      $("contextHealth").textContent = `${analysis.health}/100`;
      $("contextRul").textContent = `${analysis.rul}小时`;
      $("contextSample").textContent = `${analysis.latest.time} · 质量${analysis.quality.score}%`;
    }

    function rankedAssets(limit = assets.length) {
      return assets
        .map(asset => ({ asset, analysis: assetAnalysis(asset) }))
        .sort((a, b) => {
          const riskWeight = { red: 0, amber: 1, green: 2 };
          return riskWeight[a.analysis.risk] - riskWeight[b.analysis.risk]
            || a.analysis.health - b.analysis.health
            || a.analysis.rul - b.analysis.rul;
        })
        .slice(0, limit);
    }

    function renderDashboardRiskRank() {
      const ranked = rankedAssets(5);

      $("riskRankList").innerHTML = ranked.map(({ asset, analysis }, index) => `
        <div class="rank-item" role="button" tabindex="0" data-asset-id="${asset.id}" data-asset-view="profile" aria-label="查看${asset.name}设备画像">
          <div>
            <strong>${index + 1}. ${asset.name}</strong>
            <p>${asset.type} · 健康分 ${analysis.health} · RUL ${analysis.rul}小时 · 异常指数 ${analysis.anomalyIndex}</p>
            <span class="inline-action">查看设备画像</span>
          </div>
          <span class="pill ${analysis.risk}">${analysis.riskText}</span>
        </div>
      `).join("");
    }

    function renderDashboardMatrix() {
      $("healthMatrix").innerHTML = rankedAssets().map(({ asset, analysis }) => `
        <div class="matrix-item" role="button" tabindex="0" data-asset-id="${asset.id}" data-asset-view="profile" aria-label="查看${asset.name}健康详情">
          <div class="matrix-head">
            <strong>${asset.name}</strong>
            <span class="pill ${analysis.risk}">${analysis.riskText}</span>
          </div>
          <p>${asset.type} · ${asset.location}</p>
          <div class="matrix-meter" aria-label="健康分${analysis.health}">
            <i class="${analysis.risk}" style="width:${analysis.health}%"></i>
          </div>
          <div class="item-meta">
            <span>健康 <b>${analysis.health}</b></span>
            <span>RUL <b>${analysis.rul}h</b></span>
            <span>异常 <b>${analysis.anomalyIndex}</b></span>
          </div>
        </div>
      `).join("");
    }

    function renderDashboardActions() {
      const items = rankedAssets(4).map(({ asset, analysis }) => {
        const priority = priorityFromAnalysis(analysis);
        const targetView = analysis.risk === "green" ? "profile" : "diagnosis";
        const action = analysis.risk === "red"
          ? "立即诊断并生成工单"
          : analysis.risk === "amber"
            ? "复核趋势并准备维护"
            : "查看画像并保留基线";
        const evidence = analysis.evidence[0] ? analysis.evidence[0].title : "当前未触发高危证据";
        return { asset, analysis, priority, targetView, action, evidence };
      });

      $("actionQueue").innerHTML = items.map(({ asset, analysis, priority, targetView, action, evidence }) => `
        <div class="action-item" role="button" tabindex="0" data-asset-id="${asset.id}" data-asset-view="${targetView}" aria-label="${action}：${asset.name}">
          <div class="action-head">
            <strong>${asset.name}</strong>
            <span class="pill ${analysis.risk}">${priority}</span>
          </div>
          <p>${evidence}</p>
          <div class="item-meta">
            <span>责任人 <b>${asset.owner}</b></span>
            <span>置信度 <b>${analysis.confidence}%</b></span>
          </div>
          <span class="inline-action">${action}</span>
        </div>
      `).join("");
    }

    function renderSystemCapabilities() {
      const selectedAnalysis = assetAnalysis(assets[selectedIndex]);
      const pendingOrders = orders.filter(item => item.status !== "已完成").length;
      const avgQuality = Math.round(assets
        .map(asset => assetAnalysis(asset).quality.score)
        .reduce((sum, score) => sum + score, 0) / assets.length);
      const capabilities = [
        ["profile", "设备画像", `${assets.length}台设备档案、阈值、传感器和寿命周期统一建模。`, "查看矩阵"],
        ["diagnosis", "AI诊断", `当前设备置信度${selectedAnalysis.confidence}%，可输出证据和知识库命中。`, "运行诊断"],
        ["orders", "工单闭环", `${pendingOrders}张待处理工单，支持优先级、备件和验收标准。`, "查看工单"],
        ["data", "数据处理", `平均数据质量${avgQuality}%，覆盖采样、越界、特征和RUL链路。`, "查看链路"]
      ];

      $("systemCapabilityList").innerHTML = capabilities.map(([view, title, desc, action]) => `
        <div class="pipeline-item" role="button" tabindex="0" data-view-jump="${view}" aria-label="${action}">
          <strong>${title}</strong>
          <p>${desc}</p>
          <span class="inline-action">${action}</span>
        </div>
      `).join("");
    }

    function renderProfile(asset, analysis) {
      $("profileGrid").innerHTML = `
        <div class="profile-item"><strong>资产编号</strong><p>${asset.id}</p></div>
        <div class="profile-item"><strong>设备类型</strong><p>${asset.type}</p></div>
        <div class="profile-item"><strong>安装位置</strong><p>${asset.location}</p></div>
        <div class="profile-item"><strong>责任人</strong><p>${asset.owner}</p></div>
        <div class="profile-item"><strong>维护周期</strong><p>${asset.maintenanceCycle}小时，已运行${asset.lastMaintenanceHours}小时</p></div>
        <div class="profile-item"><strong>基准寿命</strong><p>${asset.baseLifeHours}小时，当前估计RUL为${analysis.rul}小时</p></div>
      `;

      $("thresholdRows").innerHTML = Object.keys(metricMeta).map(key => {
        const rule = asset.thresholds[key];
        return `
          <tr>
            <td>${metricMeta[key].label}</td>
            <td>${formatMetric(key, rule.min, rule)}</td>
            <td>${formatMetric(key, rule.warn, rule)}</td>
            <td>${formatMetric(key, rule.danger, rule)}</td>
            <td>${formatMetric(key, rule.max, rule)}</td>
          </tr>
        `;
      }).join("");
    }

    function rootCauses(asset, analysis) {
      const keys = analysis.evidence.map(item => item.key);
      const causes = [
        {
          name: asset.type === "动力设备" ? "滤芯堵塞或散热不足" : "轴承磨损或润滑不足",
          score: 35 + (keys.includes("vibration") ? 22 : 0) + (keys.includes("coupling") ? 28 : 0) + (keys.includes("temperature") ? 10 : 0),
          basis: "由振动、温升和耦合趋势综合判断。"
        },
        {
          name: "负载异常或工况偏离",
          score: 24 + (keys.includes("load") ? 34 : 0) + (keys.includes("current") ? 14 : 0),
          basis: "由负载率、电流偏离和维护周期剩余量判断。"
        },
        {
          name: "传感器漂移或采集异常",
          score: 18 + (analysis.quality.score < 95 ? 30 : 0),
          basis: "由数据质量、越界字段和采样完整性判断。"
        },
        {
          name: "正常老化趋势",
          score: 20 + Math.max(0, Math.round(Math.abs(Math.min(analysis.healthSlope, 0)) * 6)),
          basis: "由健康分下降斜率和维护周期运行小时判断。"
        }
      ];
      return causes
        .map(item => ({ ...item, score: clamp(item.score, 8, 96) }))
        .sort((a, b) => b.score - a.score)
        .slice(0, 4);
    }

    function renderRootCauses(asset, analysis) {
      $("rootCauseList").innerHTML = rootCauses(asset, analysis).map(item => `
        <div class="root-item">
          <strong>${item.name} · ${item.score}%</strong>
          <p>${item.basis}</p>
        </div>
      `).join("");
    }

    function renderOrderStats() {
      const total = orders.length;
      const done = orders.filter(item => item.status === "已完成").length;
      const pending = orders.filter(item => item.status !== "已完成").length;
      const urgent = orders.filter(item => item.priority === "P1 紧急" && item.status !== "已完成").length;
      const completion = total ? Math.round(done / total * 100) : 0;
      $("orderStats").innerHTML = `
        <div class="quality-item"><strong>工单总数</strong><p>${total} 条，包含AI生成与人工审核任务。</p></div>
        <div class="quality-item"><strong>待处理</strong><p>${pending} 条，其中P1紧急 ${urgent} 条。</p></div>
        <div class="quality-item"><strong>闭环率</strong><p>${completion}%，完成后自动记录验收与复盘说明。</p></div>
        <div class="quality-item"><strong>知识回写</strong><p>${done} 条已完成工单可转为维修案例，进入知识库审核。</p></div>
      `;
    }

    function renderDataProcessing(asset, analysis) {
      $("qualityList").innerHTML = `
        <div class="quality-item"><strong>有效字段</strong><p>${analysis.quality.total - analysis.quality.invalid}/${analysis.quality.total}，缺失字段 ${analysis.quality.missing}。</p></div>
        <div class="quality-item"><strong>质量评分</strong><p>${analysis.quality.score}%，综合字段合法性和采样完整性。</p></div>
        <div class="quality-item"><strong>采样窗口</strong><p>${asset.samples[0][0]} - ${asset.samples[asset.samples.length - 1][0]}，共${asset.samples.length}个点。</p></div>
        <div class="quality-item"><strong>特征输出</strong><p>健康分${analysis.health}，斜率${analysis.healthSlope.toFixed(2)}，异常指数${analysis.anomalyIndex}。</p></div>
      `;

      $("pipelineList").innerHTML = [
        ["采集", "设备网关、CSV或人工录入样例数据。"],
        ["清洗", "校验缺失值、物理越界值和采样窗口完整性。"],
        ["特征", "计算阈值偏离、趋势斜率、异常指数和健康分。"],
        ["入模", "将结构化特征输入诊断智能体和工单策略。"]
      ].map(item => `
        <div class="pipeline-item">
          <strong>${item[0]}</strong>
          <p>${item[1]}</p>
        </div>
      `).join("");
    }

    function renderMetrics() {
      const analyses = assets.map(assetAnalysis);
      const avg = Math.round(analyses.reduce((sum, item) => sum + item.health, 0) / analyses.length);
      const highRisk = analyses.filter(item => item.risk === "red").length;
      const quality = Math.round(analyses.reduce((sum, item) => sum + item.quality.score, 0) / analyses.length);
      const pendingOrders = orders.filter(item => item.status !== "已完成").length;
      $("metricDevices").textContent = assets.length;
      $("metricScore").textContent = avg;
      $("metricRisk").textContent = highRisk;
      $("metricQuality").textContent = `${quality}%`;
      $("metricOrders").textContent = pendingOrders;
    }

    function renderDeviceList() {
      $("deviceList").innerHTML = "";
      assets.forEach((asset, index) => {
        const analysis = assetAnalysis(asset);
        const item = document.createElement("div");
        item.className = `device ${index === selectedIndex ? "active" : ""}`;
        item.setAttribute("role", "button");
        item.setAttribute("tabindex", "0");
        item.innerHTML = `
          <div>
            <h3>${asset.name}</h3>
            <p>${asset.type} · ${asset.location}</p>
            <p>健康分 ${analysis.health}，RUL ${analysis.rul}小时，异常指数 ${analysis.anomalyIndex}</p>
          </div>
          <span class="pill ${analysis.risk}">${analysis.riskText}</span>
        `;
        item.addEventListener("click", () => {
          selectedIndex = index;
          renderAll(false);
        });
        item.addEventListener("keydown", event => {
          if (event.key === "Enter" || event.key === " ") {
            event.preventDefault();
            selectedIndex = index;
            renderAll(false);
          }
        });
        $("deviceList").appendChild(item);
      });
    }

    function renderSelectedAsset() {
      const asset = assets[selectedIndex];
      const analysis = assetAnalysis(asset);
      const latest = analysis.latest;
      $("selectedTitle").textContent = asset.name;
      $("selectedMeta").textContent = `${asset.type} · ${asset.location} · 责任人：${asset.owner}`;
      $("selectedRisk").textContent = analysis.riskText;
      $("selectedRisk").className = `pill ${analysis.risk}`;
      $("confidencePill").textContent = `置信度 ${analysis.confidence}%`;
      $("confidencePill").className = `pill ${analysis.confidence >= 85 ? "green" : analysis.confidence >= 70 ? "amber" : "red"}`;

      $("sensorGrid").innerHTML = Object.keys(metricMeta).map(key => {
        const threshold = asset.thresholds[key];
        const value = latest[key];
        const className = value >= threshold.danger ? "red" : value >= threshold.warn ? "amber" : "green";
        return `
          <div class="sensor">
            <span>${metricMeta[key].label}</span>
            <strong>${formatMetric(key, value, threshold)}</strong>
            <small class="pill ${className}" style="display:inline-block;margin-top:7px;">预警 ${formatMetric(key, threshold.warn, threshold)}</small>
          </div>
        `;
      }).join("");

      $("detailGrid").innerHTML = `
        <div class="detail"><span>剩余寿命RUL</span><strong>${analysis.rul}小时</strong></div>
        <div class="detail"><span>健康分斜率</span><strong>${analysis.healthSlope.toFixed(2)} 分/点</strong></div>
        <div class="detail"><span>异常指数</span><strong>${analysis.anomalyIndex}/100</strong></div>
        <div class="detail"><span>数据质量</span><strong>${analysis.quality.score}%</strong></div>
      `;

      drawHealthChart($("healthCanvas"), analysis.healthSeries);
      drawRiskChart($("riskCanvas"), asset, analysis);
      renderSampleRows(asset);
      renderRiskSummary(asset, analysis);
      renderEvidence(analysis);
      renderKnowledge(analysis);
      renderWorkflow(asset, analysis);
      renderProfile(asset, analysis);
      renderRootCauses(asset, analysis);
      renderDataProcessing(asset, analysis);
    }

    function renderRiskSummary(asset, analysis) {
      $("riskSummary").innerHTML = `
        <div class="detail"><span>工单优先级</span><strong>${priorityFromAnalysis(analysis)}</strong></div>
        <div class="detail"><span>知识命中</span><strong>${analysis.matches.length} 条</strong></div>
        <div class="detail"><span>危险证据</span><strong>${analysis.evidence.filter(item => item.level === "danger").length} 条</strong></div>
        <div class="detail"><span>维护周期剩余</span><strong>${Math.max(asset.maintenanceCycle - asset.lastMaintenanceHours, 0)}小时</strong></div>
      `;
    }

    function renderEvidence(analysis) {
      const evidence = analysis.evidence.length ? analysis.evidence : [{
        level: "ok",
        title: "未触发异常证据",
        detail: "最新采样点低于预警阈值，健康分趋势稳定。"
      }];
      $("evidenceList").innerHTML = evidence.map(item => `
        <div class="evidence">
          <div>
            <strong>${item.title}</strong>
            <span>${item.detail}</span>
          </div>
          <span class="pill ${riskBadge(item.level)}">${item.level === "danger" ? "危险" : item.level === "warn" ? "预警" : "正常"}</span>
        </div>
      `).join("");
    }

    function renderKnowledge(analysis) {
      $("knowledgeList").innerHTML = analysis.matches.map(item => `
        <div class="knowledge-item">
          <strong>${item.id} · ${item.title}</strong>
          <p>匹配分 ${item.score}。建议：${item.action}</p>
          <p>安全要求：${item.safety}</p>
        </div>
      `).join("") || `
        <div class="knowledge-item">
          <strong>未命中高相关知识</strong>
          <p>建议补充该设备的说明书、维修案例和安全规范后重新训练知识库。</p>
        </div>
      `;
    }

    function renderWorkflow(asset, analysis) {
      const top = analysis.matches[0];
      const steps = [
        ["数据监测", `读取${asset.samples.length}个采样点，最新时间${analysis.latest.time}。`],
        ["质量校验", `数据质量${analysis.quality.score}%，无效字段${analysis.quality.invalid}/${analysis.quality.total}。`],
        ["异常识别", `健康分${analysis.health}，风险等级${analysis.riskText}，异常指数${analysis.anomalyIndex}。`],
        ["知识检索", top ? `命中${top.id}，匹配分${top.score}。` : "未命中强相关知识条目。"],
        ["运维决策", `${recommendation(asset, analysis)} 工单优先级为${priorityFromAnalysis(analysis)}。`]
      ];
      $("workflowList").innerHTML = steps.map((item, index) => `
        <div class="workflow-step">
          <div class="step-index">${index + 1}</div>
          <div><strong>${item[0]}</strong><span>${item[1]}</span></div>
        </div>
      `).join("");
    }

    function renderDiagnosis(forceText) {
      const asset = assets[selectedIndex];
      const analysis = assetAnalysis(asset);
      const top = analysis.matches[0];
      lastDiagnosis = { assetId: asset.id, analysis };
      $("diagnosisBox").innerHTML = `
        <strong>诊断结论</strong>
        ${asset.name}当前为${analysis.riskText}，健康分${analysis.health}，预计剩余可运行时间${analysis.rul}小时，诊断置信度${analysis.confidence}%。
        ${analysis.evidence.length ? `主要依据为${analysis.evidence.slice(0, 2).map(item => item.title).join("、")}。` : "当前未发现显著异常。"}
        ${top ? `知识库最高命中为“${top.title}”。` : ""}
        ${recommendation(asset, analysis)}
      `;
      if (forceText) renderAll(false);
    }

    function renderOrders() {
      if (!orders.length) {
        $("orderList").innerHTML = `
          <div class="order">
            <strong>暂无工单</strong>
            <p>运行AI诊断后，可根据风险等级生成维护工单。</p>
          </div>
        `;
        renderOrderStats();
        return;
      }
      const priorityRank = { "P1 紧急": 1, "P2 优先": 2, "P3 常规": 3 };
      const sorted = [...orders].sort((a, b) => (priorityRank[a.priority] || 9) - (priorityRank[b.priority] || 9));
      $("orderList").innerHTML = sorted.map(order => `
        <div class="order">
          <strong>${order.id} · ${order.title}</strong>
          <div class="order-row"><span>设备编号</span><b>${order.assetId}</b></div>
          <div class="order-row"><span>优先级</span><b>${order.priority}</b></div>
          <div class="order-row"><span>状态</span><b>${order.status}</b></div>
          <div class="order-row"><span>推荐备件</span><b>${order.parts}</b></div>
          <p>验收标准：${order.acceptance}</p>
        </div>
      `).join("");
      renderOrderStats();
    }

    function createOrder() {
      const asset = assets[selectedIndex];
      const analysis = assetAnalysis(asset);
      lastDiagnosis = { assetId: asset.id, analysis };
      const top = analysis.matches[0];
      const priority = priorityFromAnalysis(analysis);
      const parts = suggestParts(asset, analysis);
      const id = `WO-20260610-${String(orders.length + 1).padStart(3, "0")}`;
      orders.unshift({
        id,
        assetId: asset.id,
        title: `${asset.name}${analysis.riskText}专项维护`,
        priority,
        status: "待审核",
        parts,
        acceptance: acceptanceText(asset, analysis),
        knowledge: top ? top.id : "待补充"
      });
      renderDiagnosis(false);
      renderAll(false);
    }

    function suggestParts(asset, analysis) {
      const keys = analysis.evidence.map(item => item.key);
      if (asset.type === "动力设备") return "滤芯、润滑油、密封圈、温度传感器";
      if (keys.includes("vibration") || keys.includes("coupling")) return "轴承组件、润滑脂、紧固件、振动传感器";
      if (keys.includes("temperature")) return "温控模块、热敏电阻、散热风扇";
      if (keys.includes("current") || keys.includes("load")) return "电机接插件、驱动模块、保险件";
      return "常规润滑耗材、清洁耗材";
    }

    function acceptanceText(asset, analysis) {
      if (analysis.risk === "red") {
        return "试运行30分钟后健康分大于82，危险阈值零触发，异常指数低于35。";
      }
      if (analysis.risk === "amber") {
        return "连续两次采样健康分大于84，预警项数量不增加。";
      }
      return "完成巡检记录，关键指标保持在预警阈值以下。";
    }

    function closeTopOrder() {
      const openOrder = orders.find(item => item.status !== "已完成");
      if (openOrder) {
        openOrder.status = "已完成";
        openOrder.acceptance += " 已记录维修复盘并回写知识库。";
      }
      renderAll(false);
    }

    function renderSampleRows(asset) {
      $("sampleRows").innerHTML = asset.samples.map(sample => {
        const health = sampleHealth(asset, sample);
        const anomaly = 100 - health;
        const cls = health < 70 ? "red" : health < 82 ? "amber" : "green";
        const text = health < 70 ? "危险" : health < 82 ? "预警" : "正常";
        return `
          <tr>
            <td>${sample[0]}</td>
            <td>${sample[1].toFixed(1)}</td>
            <td>${sample[2].toFixed(1)}</td>
            <td>${sample[3].toFixed(1)}</td>
            <td>${Math.round(sample[4] * 100)}%</td>
            <td>${health}</td>
            <td>${anomaly}</td>
            <td><span class="pill ${cls}">${text}</span></td>
          </tr>
        `;
      }).join("");
    }

    function drawHealthChart(canvas, series) {
      const ctx = canvas.getContext("2d");
      const width = canvas.width;
      const height = canvas.height;
      ctx.clearRect(0, 0, width, height);
      const bg = ctx.createLinearGradient(0, 0, 0, height);
      bg.addColorStop(0, "#07141a");
      bg.addColorStop(1, "#020406");
      ctx.fillStyle = bg;
      ctx.fillRect(0, 0, width, height);

      ctx.strokeStyle = "rgba(148, 163, 184, 0.18)";
      ctx.lineWidth = 1;
      for (let i = 0; i < 5; i++) {
        const y = 42 + i * 56;
        ctx.beginPath();
        ctx.moveTo(54, y);
        ctx.lineTo(width - 34, y);
        ctx.stroke();
      }

      drawThresholdLine(ctx, width, height, 82, "#f59e0b", "中风险线 82");
      drawThresholdLine(ctx, width, height, 70, "#fb7185", "高风险线 70");

      const points = series.map((value, index) => {
        const x = 62 + index * ((width - 110) / (series.length - 1));
        const y = scaleHealthY(value, height);
        return [x, y, value];
      });

      const gradient = ctx.createLinearGradient(0, 0, width, 0);
      gradient.addColorStop(0, "#2dd4bf");
      gradient.addColorStop(0.58, "#38bdf8");
      gradient.addColorStop(1, "#a78bfa");
      ctx.strokeStyle = gradient;
      ctx.lineWidth = 4;
      ctx.shadowColor = "rgba(56, 189, 248, 0.35)";
      ctx.shadowBlur = 12;
      ctx.beginPath();
      points.forEach(([x, y], index) => {
        if (index === 0) ctx.moveTo(x, y);
        else ctx.lineTo(x, y);
      });
      ctx.stroke();
      ctx.shadowBlur = 0;

      points.forEach(([x, y, value]) => {
        ctx.fillStyle = "#07111f";
        ctx.strokeStyle = value < 70 ? "#fb7185" : value < 82 ? "#f59e0b" : "#2dd4bf";
        ctx.lineWidth = 3;
        ctx.beginPath();
        ctx.arc(x, y, 6, 0, Math.PI * 2);
        ctx.fill();
        ctx.stroke();
        ctx.fillStyle = "#dbeafe";
        ctx.font = "13px Fira Code, Microsoft YaHei";
        ctx.fillText(value, x - 8, y - 12);
      });

      ctx.fillStyle = "#cbd5e1";
      ctx.font = "14px Fira Sans, Microsoft YaHei";
      ctx.fillText("近8次采样健康分", 54, 24);
    }

    function scaleHealthY(value, height) {
      return height - 38 - ((value - 40) / 60) * (height - 78);
    }

    function drawThresholdLine(ctx, width, height, value, color, label) {
      const y = scaleHealthY(value, height);
      ctx.strokeStyle = color;
      ctx.setLineDash([6, 5]);
      ctx.lineWidth = 1.5;
      ctx.beginPath();
      ctx.moveTo(54, y);
      ctx.lineTo(width - 34, y);
      ctx.stroke();
      ctx.setLineDash([]);
      ctx.fillStyle = color;
      ctx.font = "12px Microsoft YaHei";
      ctx.fillText(label, width - 150, y - 7);
    }

    function drawRiskChart(canvas, asset, analysis) {
      const ctx = canvas.getContext("2d");
      const width = canvas.width;
      const height = canvas.height;
      const latest = analysis.latest;
      const data = Object.keys(metricMeta).map(key => {
        const threshold = asset.thresholds[key];
        const ratio = clamp(latest[key] / threshold.danger, 0, 1.25);
        return {
          label: metricMeta[key].label,
          value: Math.round(ratio * 100),
          color: ratio >= 1 ? "#fb7185" : ratio >= 0.85 ? "#f59e0b" : "#2dd4bf"
        };
      });
      ctx.clearRect(0, 0, width, height);
      const bg = ctx.createLinearGradient(0, 0, 0, height);
      bg.addColorStop(0, "#07141a");
      bg.addColorStop(1, "#020406");
      ctx.fillStyle = bg;
      ctx.fillRect(0, 0, width, height);
      ctx.fillStyle = "#cbd5e1";
      ctx.font = "14px Fira Sans, Microsoft YaHei";
      ctx.fillText("最新值占危险阈值比例", 42, 30);

      data.forEach((item, index) => {
        const barWidth = 104;
        const gap = 76;
        const x = 70 + index * (barWidth + gap);
        const barHeight = (item.value / 125) * 210;
        const y = height - 48 - barHeight;
        ctx.fillStyle = "rgba(148, 163, 184, 0.11)";
        ctx.fillRect(x, height - 258, barWidth, 210);
        const barGradient = ctx.createLinearGradient(0, y, 0, height - 48);
        barGradient.addColorStop(0, item.color);
        barGradient.addColorStop(1, "rgba(56, 189, 248, 0.22)");
        ctx.fillStyle = barGradient;
        ctx.fillRect(x, y, barWidth, barHeight);
        ctx.strokeStyle = "rgba(255, 255, 255, 0.12)";
        ctx.strokeRect(x, height - 258, barWidth, 210);
        ctx.fillStyle = "#f8fafc";
        ctx.font = "bold 18px Fira Code, Microsoft YaHei";
        ctx.fillText(`${item.value}%`, x + 27, y - 10);
        ctx.fillStyle = "#93a4ba";
        ctx.font = "13px Fira Sans, Microsoft YaHei";
        ctx.fillText(item.label, x + 19, height - 18);
      });
    }

    function injectHighRisk() {
      const target = assets.find(item => item.id === "CNC-01");
      target.samples = [
        ["09:00", 58.0, 2.6, 15.8, 0.66],
        ["09:10", 61.4, 3.0, 16.4, 0.70],
        ["09:20", 64.9, 3.4, 17.2, 0.74],
        ["09:30", 68.5, 3.9, 18.3, 0.79],
        ["09:40", 72.6, 4.4, 19.4, 0.83],
        ["09:50", 76.1, 4.9, 20.8, 0.87],
        ["10:00", 79.4, 5.4, 22.2, 0.91],
        ["10:10", 82.3, 5.9, 23.0, 0.94]
      ];
      target.lastMaintenanceHours = 228;
      selectedIndex = assets.findIndex(item => item.id === "CNC-01");
      renderDiagnosis(false);
      renderAll(false);
      switchView("profile");
    }

    function resetBaseline() {
      assets = cloneAssets(baselineAssets);
      selectedIndex = 0;
      orders = [
        {
          id: "WO-20260610-001",
          assetId: "ACP-03",
          title: "空压机高温趋势复核",
          priority: "P2 优先",
          status: "待执行",
          parts: "滤芯、润滑油、密封圈",
          acceptance: "温度回落至72℃以下，电流低于20A"
        }
      ];
      lastDiagnosis = null;
      $("diagnosisBox").innerHTML = `
        <strong>诊断结论</strong>
        点击“运行AI诊断”后生成结构化诊断报告。
      `;
      renderAll(false);
    }

    function renderAll(includeDiagnosis) {
      renderMetrics();
      renderContextStrip();
      renderDashboardRiskRank();
      renderDashboardMatrix();
      renderDashboardActions();
      renderSystemCapabilities();
      renderDeviceList();
      renderSelectedAsset();
      renderOrders();
      if (includeDiagnosis) renderDiagnosis(false);
      renderPageChrome();
    }

    function selectAssetById(assetId) {
      const index = assets.findIndex(item => item.id === assetId);
      if (index >= 0) {
        selectedIndex = index;
        renderAll(false);
        return true;
      }
      return false;
    }

    function openAssetView(assetId, view) {
      if (!selectAssetById(assetId)) return;
      if (view === "diagnosis") renderDiagnosis(false);
      switchView(viewConfig[view] ? view : "profile");
    }

    function openWorstAsset() {
      const top = rankedAssets(1)[0];
      if (top) openAssetView(top.asset.id, "profile");
    }

    function runDashboardAction(action) {
      if (action === "profile") {
        switchView("profile");
      } else if (action === "selected-profile") {
        switchView("profile");
      } else if (action === "worst-profile") {
        openWorstAsset();
      } else if (action === "diagnosis") {
        renderDiagnosis(false);
        switchView("diagnosis");
      } else if (viewConfig[action]) {
        switchView(action);
      }
    }

    function activateDashboardElement(element) {
      const assetId = element.dataset.assetId;
      if (assetId) {
        openAssetView(assetId, element.dataset.assetView || "profile");
        return;
      }
      if (element.dataset.viewJump) {
        runDashboardAction(element.dataset.viewJump);
        return;
      }
      if (element.dataset.dashboardAction) {
        runDashboardAction(element.dataset.dashboardAction);
      }
    }

    $("baselineBtn").addEventListener("click", resetBaseline);
    $("injectBtn").addEventListener("click", injectHighRisk);
    $("diagnoseBtn").addEventListener("click", () => {
      renderDiagnosis(true);
      switchView("diagnosis");
    });
    $("orderBtn").addEventListener("click", () => {
      createOrder();
      switchView("orders");
    });
    $("closeOrderBtn").addEventListener("click", closeTopOrder);
    document.querySelectorAll("[data-view-target]").forEach(button => {
      button.addEventListener("click", () => switchView(button.dataset.viewTarget));
    });
    document.addEventListener("click", event => {
      const target = event.target.closest("[data-asset-id], [data-view-jump], [data-dashboard-action]");
      if (target) activateDashboardElement(target);
    });
    document.addEventListener("keydown", event => {
      if (event.key !== "Enter" && event.key !== " ") return;
      const target = event.target.closest('[role="button"][data-asset-id], [role="button"][data-view-jump], [role="button"][data-dashboard-action]');
      if (!target) return;
      event.preventDefault();
      activateDashboardElement(target);
    });

    renderAll(false);
    switchView("dashboard");
  </script>
</body>
</html>
