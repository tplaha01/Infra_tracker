<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Inf₹a — Command Center</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Sans:wght@300;400;500&family=JetBrains+Mono:wght@400;500;700&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #070B14;
    --bg2: #0D1220;
    --bg3: #111827;
    --border: #1a2235;
    --border2: #243047;
    --primary: #4F46E5;
    --primary-dim: rgba(79,70,229,0.12);
    --accent: #FF9F1C;
    --accent-dim: rgba(255,159,28,0.12);
    --green: #10B981;
    --green-dim: rgba(16,185,129,0.12);
    --red: #EF4444;
    --red-dim: rgba(239,68,68,0.1);
    --yellow: #F59E0B;
    --yellow-dim: rgba(245,158,11,0.1);
    --text: #F1F5F9;
    --text2: #94A3B8;
    --text3: #475569;
    --mono: 'JetBrains Mono', monospace;
    --display: 'Syne', sans-serif;
    --body: 'DM Sans', sans-serif;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--body);
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* Grain overlay */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.03'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 0;
    opacity: 0.4;
  }

  /* Ambient glow */
  body::after {
    content: '';
    position: fixed;
    top: -20%;
    left: 30%;
    width: 600px;
    height: 600px;
    background: radial-gradient(circle, rgba(79,70,229,0.06) 0%, transparent 70%);
    pointer-events: none;
    z-index: 0;
  }

  .wrapper {
    position: relative;
    z-index: 1;
    max-width: 1100px;
    margin: 0 auto;
    padding: 0 24px 80px;
  }

  /* HEADER */
  header {
    padding: 32px 0 40px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    border-bottom: 1px solid var(--border);
    margin-bottom: 48px;
  }

  .logo {
    font-family: var(--display);
    font-size: 22px;
    font-weight: 800;
    letter-spacing: -0.5px;
    color: var(--text);
  }

  .logo span { color: var(--accent); }

  .header-meta {
    display: flex;
    align-items: center;
    gap: 16px;
  }

  .tag {
    font-family: var(--mono);
    font-size: 11px;
    padding: 4px 10px;
    border-radius: 4px;
    border: 1px solid var(--border2);
    color: var(--text2);
    letter-spacing: 0.05em;
    text-transform: uppercase;
  }

  .tag.live {
    border-color: rgba(16,185,129,0.3);
    color: var(--green);
    background: var(--green-dim);
  }

  .tag.live::before {
    content: '●';
    margin-right: 6px;
    animation: pulse 2s infinite;
  }

  @keyframes pulse {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.3; }
  }

  /* HERO STATS */
  .stats-row {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 12px;
    margin-bottom: 48px;
  }

  .stat-card {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 20px;
    position: relative;
    overflow: hidden;
    transition: border-color 0.2s;
  }

  .stat-card:hover { border-color: var(--border2); }

  .stat-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
  }

  .stat-card.primary::before { background: var(--primary); }
  .stat-card.accent::before { background: var(--accent); }
  .stat-card.green::before { background: var(--green); }
  .stat-card.yellow::before { background: var(--yellow); }

  .stat-label {
    font-family: var(--mono);
    font-size: 10px;
    color: var(--text3);
    text-transform: uppercase;
    letter-spacing: 0.1em;
    margin-bottom: 8px;
  }

  .stat-value {
    font-family: var(--display);
    font-size: 28px;
    font-weight: 700;
    line-height: 1;
    margin-bottom: 4px;
  }

  .stat-card.primary .stat-value { color: var(--primary); }
  .stat-card.accent .stat-value { color: var(--accent); }
  .stat-card.green .stat-value { color: var(--green); }
  .stat-card.yellow .stat-value { color: var(--yellow); }

  .stat-sub {
    font-size: 12px;
    color: var(--text3);
  }

  /* PHASE SECTIONS */
  .phases { display: flex; flex-direction: column; gap: 36px; }

  .phase {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 12px;
    overflow: hidden;
    animation: fadeUp 0.4s ease both;
  }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(16px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .phase:nth-child(1) { animation-delay: 0.05s; }
  .phase:nth-child(2) { animation-delay: 0.1s; }
  .phase:nth-child(3) { animation-delay: 0.15s; }
  .phase:nth-child(4) { animation-delay: 0.2s; }
  .phase:nth-child(5) { animation-delay: 0.25s; }

  .phase-header {
    padding: 20px 24px;
    display: flex;
    align-items: center;
    gap: 16px;
    border-bottom: 1px solid var(--border);
    cursor: pointer;
    user-select: none;
    transition: background 0.15s;
  }

  .phase-header:hover { background: rgba(255,255,255,0.02); }

  .phase-number {
    font-family: var(--mono);
    font-size: 11px;
    font-weight: 700;
    padding: 3px 8px;
    border-radius: 4px;
    min-width: 32px;
    text-align: center;
  }

  .phase-title {
    font-family: var(--display);
    font-size: 16px;
    font-weight: 700;
    flex: 1;
  }

  .phase-timeline {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--text3);
    padding: 3px 10px;
    border: 1px solid var(--border);
    border-radius: 4px;
  }

  .phase-progress {
    font-family: var(--mono);
    font-size: 12px;
    font-weight: 700;
    min-width: 44px;
    text-align: right;
  }

  .phase-toggle {
    font-size: 18px;
    color: var(--text3);
    transition: transform 0.2s;
    width: 20px;
    text-align: center;
  }

  .phase.collapsed .phase-toggle { transform: rotate(-90deg); }

  .progress-bar-wrap {
    height: 2px;
    background: var(--border);
  }

  .progress-bar-fill {
    height: 100%;
    border-radius: 0 2px 2px 0;
    transition: width 0.5s ease;
  }

  /* TASKS */
  .task-list {
    padding: 8px 0;
  }

  .phase.collapsed .task-list { display: none; }

  .task-group-label {
    font-family: var(--mono);
    font-size: 10px;
    color: var(--text3);
    text-transform: uppercase;
    letter-spacing: 0.1em;
    padding: 12px 24px 6px;
  }

  .task {
    display: flex;
    align-items: flex-start;
    gap: 14px;
    padding: 10px 24px;
    cursor: pointer;
    transition: background 0.12s;
    border-radius: 0;
    position: relative;
  }

  .task:hover { background: rgba(255,255,255,0.025); }

  .task.done { opacity: 0.55; }

  .checkbox {
    width: 18px;
    height: 18px;
    border-radius: 4px;
    border: 1.5px solid var(--border2);
    flex-shrink: 0;
    margin-top: 1px;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.15s;
    background: transparent;
  }

  .task.done .checkbox {
    border-color: var(--green);
    background: var(--green-dim);
  }

  .checkbox::after {
    content: '';
    display: none;
    width: 5px;
    height: 9px;
    border: 2px solid var(--green);
    border-top: none;
    border-left: none;
    transform: rotate(45deg) translateY(-1px);
  }

  .task.done .checkbox::after { display: block; }

  .task-content { flex: 1; }

  .task-name {
    font-size: 14px;
    font-weight: 500;
    color: var(--text);
    line-height: 1.4;
    transition: color 0.15s;
  }

  .task.done .task-name {
    text-decoration: line-through;
    color: var(--text3);
  }

  .task-desc {
    font-size: 12px;
    color: var(--text3);
    margin-top: 2px;
    line-height: 1.4;
  }

  .task-badge {
    font-family: var(--mono);
    font-size: 10px;
    padding: 2px 7px;
    border-radius: 3px;
    flex-shrink: 0;
    margin-top: 2px;
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }

  .badge-critical { background: var(--red-dim); color: var(--red); border: 1px solid rgba(239,68,68,0.2); }
  .badge-marketing { background: var(--accent-dim); color: var(--accent); border: 1px solid rgba(255,159,28,0.2); }
  .badge-tech { background: var(--primary-dim); color: var(--primary); border: 1px solid rgba(79,70,229,0.2); }
  .badge-legal { background: var(--yellow-dim); color: var(--yellow); border: 1px solid rgba(245,158,11,0.2); }
  .badge-growth { background: var(--green-dim); color: var(--green); border: 1px solid rgba(16,185,129,0.2); }

  /* SECTION DIVIDER */
  .section-title {
    font-family: var(--display);
    font-size: 13px;
    font-weight: 700;
    color: var(--text3);
    text-transform: uppercase;
    letter-spacing: 0.15em;
    margin-bottom: 20px;
    display: flex;
    align-items: center;
    gap: 12px;
  }

  .section-title::after {
    content: '';
    flex: 1;
    height: 1px;
    background: var(--border);
  }

  /* NOTES AREA */
  .notes-section {
    margin-top: 48px;
  }

  .notes-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
  }

  .note-card {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 20px;
  }

  .note-card h4 {
    font-family: var(--display);
    font-size: 13px;
    font-weight: 700;
    margin-bottom: 12px;
    color: var(--text2);
    text-transform: uppercase;
    letter-spacing: 0.08em;
  }

  .note-card ul {
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: 8px;
  }

  .note-card ul li {
    font-size: 13px;
    color: var(--text2);
    padding-left: 14px;
    position: relative;
    line-height: 1.5;
  }

  .note-card ul li::before {
    content: '→';
    position: absolute;
    left: 0;
    color: var(--text3);
    font-family: var(--mono);
    font-size: 11px;
  }

  /* FOOTER */
  .footer {
    margin-top: 64px;
    padding-top: 24px;
    border-top: 1px solid var(--border);
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .footer-brand {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--text3);
  }

  .footer-brand span { color: var(--accent); }

  .last-updated {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--text3);
  }

  /* RESET BTN */
  .reset-btn {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--text3);
    background: none;
    border: 1px solid var(--border);
    padding: 5px 12px;
    border-radius: 4px;
    cursor: pointer;
    transition: all 0.15s;
  }

  .reset-btn:hover {
    color: var(--red);
    border-color: rgba(239,68,68,0.3);
  }

  /* RESPONSIVE */
  @media (max-width: 768px) {
    .stats-row { grid-template-columns: 1fr 1fr; }
    .notes-grid { grid-template-columns: 1fr; }
    .phase-timeline { display: none; }
    header { flex-direction: column; gap: 16px; align-items: flex-start; }
  }

  @media (max-width: 480px) {
    .stats-row { grid-template-columns: 1fr 1fr; }
    .stat-value { font-size: 22px; }
  }
</style>
</head>
<body>
<div class="wrapper">

  <header>
    <div class="logo">Inf<span>₹</span>a <span style="color:var(--text3);font-weight:400;font-size:14px;margin-left:8px;">Command Center</span></div>
    <div class="header-meta">
      <span class="tag">v0.1.0</span>
      <span class="tag live">Building</span>
      <button class="reset-btn" onclick="resetAll()">Reset All</button>
    </div>
  </header>

  <!-- STATS -->
  <div class="stats-row" id="statsRow">
    <div class="stat-card primary">
      <div class="stat-label">Total Tasks</div>
      <div class="stat-value" id="totalCount">0</div>
      <div class="stat-sub">across all phases</div>
    </div>
    <div class="stat-card green">
      <div class="stat-label">Completed</div>
      <div class="stat-value" id="doneCount">0</div>
      <div class="stat-sub">tasks done</div>
    </div>
    <div class="stat-card accent">
      <div class="stat-label">Progress</div>
      <div class="stat-value" id="progressPct">0%</div>
      <div class="stat-sub">overall completion</div>
    </div>
    <div class="stat-card yellow">
      <div class="stat-label">Phase</div>
      <div class="stat-value" id="currentPhase">01</div>
      <div class="stat-sub">currently active</div>
    </div>
  </div>

  <!-- PHASES -->
  <div class="section-title">Roadmap & Execution Plan</div>

  <div class="phases" id="phasesContainer">

    <!-- PHASE 0 -->
    <div class="phase" id="phase-0">
      <div class="phase-header" onclick="togglePhase('phase-0')">
        <span class="phase-number" style="background:var(--accent-dim);color:var(--accent)">P0</span>
        <span class="phase-title">Foundation & Legal</span>
        <span class="phase-timeline">Month 0–1</span>
        <span class="phase-progress" id="prog-phase-0" style="color:var(--accent)">0%</span>
        <span class="phase-toggle">▾</span>
      </div>
      <div class="progress-bar-wrap"><div class="progress-bar-fill" id="bar-phase-0" style="background:var(--accent);width:0%"></div></div>
      <div class="task-list">
        <div class="task-group-label">Company & Legal</div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Register Inf₹a Technologies Pvt. Ltd.</div>
            <div class="task-desc">Incorporate via StartupIndia / Razorpay Rize. Get CIN, PAN, TAN.</div>
          </div>
          <span class="task-badge badge-critical">critical</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">GST Registration</div>
            <div class="task-desc">Register for GST (mandatory for platform fee collection). 18% applicable.</div>
          </div>
          <span class="task-badge badge-legal">legal</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Open Current Account (HDFC / ICICI)</div>
            <div class="task-desc">Separate business account for settlements and payouts.</div>
          </div>
          <span class="task-badge badge-legal">legal</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Apply for Razorpay Partner Program</div>
            <div class="task-desc">Operate under Razorpay's PA license in year 1. Get reseller agreement signed.</div>
          </div>
          <span class="task-badge badge-critical">critical</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Draft Terms of Service, Privacy Policy, Refund Policy</div>
            <div class="task-desc">India-specific. Cover PDPB, RBI guidelines. Lawyer review required.</div>
          </div>
          <span class="task-badge badge-legal">legal</span>
        </div>
        <div class="task-group-label">Domain & Infrastructure</div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Register infraHQ.in domain</div>
            <div class="task-desc">Primary domain. Also grab infraHQ.com, infra-payments.in as backups.</div>
          </div>
          <span class="task-badge badge-tech">tech</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Set up Vercel + Neon + Upstash accounts</div>
            <div class="task-desc">Core infra stack. Configure Mumbai region on all services.</div>
          </div>
          <span class="task-badge badge-tech">tech</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Set up Cloudflare (DNS + R2 + CDN)</div>
            <div class="task-desc">cdn.infraHQ.in for JS SDK. R2 bucket for settlement PDFs.</div>
          </div>
          <span class="task-badge badge-tech">tech</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Set up GitHub org + Turborepo monorepo</div>
            <div class="task-desc">Repo structure as per AGENTS.md §3. Configure CI/CD via GitHub Actions.</div>
          </div>
          <span class="task-badge badge-tech">tech</span>
        </div>
      </div>
    </div>

    <!-- PHASE 1 -->
    <div class="phase collapsed" id="phase-1">
      <div class="phase-header" onclick="togglePhase('phase-1')">
        <span class="phase-number" style="background:var(--primary-dim);color:var(--primary)">P1</span>
        <span class="phase-title">Core Product — Sandbox & Dashboard</span>
        <span class="phase-timeline">Month 1–3</span>
        <span class="phase-progress" id="prog-phase-1" style="color:var(--primary)">0%</span>
        <span class="phase-toggle">▾</span>
      </div>
      <div class="progress-bar-wrap"><div class="progress-bar-fill" id="bar-phase-1" style="background:var(--primary);width:0%"></div></div>
      <div class="task-list">
        <div class="task-group-label">Auth & Onboarding</div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Build signup / login (email + Google OAuth)</div>
            <div class="task-desc">NextAuth v5. Email verification via Resend. JWT sessions.</div>
          </div>
          <span class="task-badge badge-tech">tech</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">5-step KYC onboarding wizard</div>
            <div class="task-desc">PAN, GST, bank account, business type. Persist progress in DB.</div>
          </div>
          <span class="task-badge badge-tech">tech</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Auto-generate sandbox API keys on signup</div>
            <div class="task-desc">infra_test_sk_* prefix. Show in dashboard immediately.</div>
          </div>
          <span class="task-badge badge-tech">tech</span>
        </div>
        <div class="task-group-label">Payment Core</div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Razorpay integration — payment creation, capture, refund</div>
            <div class="task-desc">InfraGateway service class wrapping Razorpay SDK. Error normalization.</div>
          </div>
          <span class="task-badge badge-tech">tech</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Webhook engine — BullMQ + HMAC signing</div>
            <div class="task-desc">X-Infra-Signature-256. Exponential backoff, 72h retry window.</div>
          </div>
          <span class="task-badge badge-tech">tech</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Payment links + QR code generation</div>
            <div class="task-desc">Shareable URLs, expiry, amount-locked / open. QR via qrcode lib.</div>
          </div>
          <span class="task-badge badge-tech">tech</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Hosted checkout page (white-labeled)</div>
            <div class="task-desc">Merchant branding. Mobile-first. Inf₹a badge in footer.</div>
          </div>
          <span class="task-badge badge-tech">tech</span>
        </div>
        <div class="task-group-label">Merchant Dashboard</div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Revenue graph (real-time, date ranges)</div>
            <div class="task-desc">7d/30d/90d/custom. Recharts or Chart.js. Dark theme.</div>
          </div>
          <span class="task-badge badge-tech">tech</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Transaction table with filters</div>
            <div class="task-desc">Status, method, amount, date. Pagination. CSV export.</div>
          </div>
          <span class="task-badge badge-tech">tech</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">API key management UI</div>
            <div class="task-desc">Create, rotate, scope, IP allowlist. Show last used / usage stats.</div>
          </div>
          <span class="task-badge badge-tech">tech</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Sandbox environment + payment simulator</div>
            <div class="task-desc">Trigger success/failure/timeout. Amber sandbox banner. Isolated Neon branch.</div>
          </div>
          <span class="task-badge badge-tech">tech</span>
        </div>
        <div class="task-group-label">SDK & API</div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">REST API v1 — payments, refunds, webhooks</div>
            <div class="task-desc">tRPC routers exposed as REST. Zod validation. OpenAPI spec.</div>
          </div>
          <span class="task-badge badge-tech">tech</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">@infra-payments/node SDK v0.1</div>
            <div class="task-desc">InfraClient class. payments.create(), refunds.create(), webhooks.constructEvent().</div>
          </div>
          <span class="task-badge badge-tech">tech</span>
        </div>
      </div>
    </div>

    <!-- PHASE 2 -->
    <div class="phase collapsed" id="phase-2">
      <div class="phase-header" onclick="togglePhase('phase-2')">
        <span class="phase-number" style="background:var(--green-dim);color:var(--green)">P2</span>
        <span class="phase-title">Landing Page & First Merchants</span>
        <span class="phase-timeline">Month 2–3</span>
        <span class="phase-progress" id="prog-phase-2" style="color:var(--green)">0%</span>
        <span class="phase-toggle">▾</span>
      </div>
      <div class="progress-bar-wrap"><div class="progress-bar-fill" id="bar-phase-2" style="background:var(--green);width:0%"></div></div>
      <div class="task-list">
        <div class="task-group-label">Landing Page</div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Build all 11 landing page sections</div>
            <div class="task-desc">Hero, trust bar, features, pricing, code demo, sandbox CTA, DX, testimonials, FAQ, CTA, footer.</div>
          </div>
          <span class="task-badge badge-tech">tech</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">SEO: JSON-LD, sitemap, OG images, meta</div>
            <div class="task-desc">Organization + SoftwareApplication + FAQPage schemas. next-sitemap.</div>
          </div>
          <span class="task-badge badge-marketing">marketing</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Lighthouse ≥ 90 on all metrics</div>
            <div class="task-desc">LCP &lt;2.5s, CLS &lt;0.1, INP &lt;200ms. Vercel Speed Insights.</div>
          </div>
          <span class="task-badge badge-tech">tech</span>
        </div>
        <div class="task-group-label">Marketing Channels</div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Twitter / X account — @infraHQ</div>
            <div class="task-desc">Build in public. Post weekly dev logs. Target Indian startup Twitter.</div>
          </div>
          <span class="task-badge badge-marketing">marketing</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">ProductHunt launch preparation</div>
            <div class="task-desc">Assets, hunter outreach, launch day playbook. Target #1 Product of the Day.</div>
          </div>
          <span class="task-badge badge-marketing">marketing</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Post in IndieHackers, Hacker News (Show HN)</div>
            <div class="task-desc">"We built a Stripe for India" angle. Link sandbox demo.</div>
          </div>
          <span class="task-badge badge-marketing">marketing</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Onboard first 10 beta merchants (friends/network)</div>
            <div class="task-desc">Manual onboarding OK. Collect feedback aggressively. Waive commission for 3 months.</div>
          </div>
          <span class="task-badge badge-growth">growth</span>
        </div>
        <div class="task-group-label">Content SEO</div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Write 5 SEO blog posts</div>
            <div class="task-desc">"How to accept UPI payments in Node.js", "Razorpay vs Cashfree vs Inf₹a", "Payment gateway India guide 2025"</div>
          </div>
          <span class="task-badge badge-marketing">marketing</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Publish documentation site (Fumadocs)</div>
            <div class="task-desc">5-min quickstart, API reference, sandbox guide. infraHQ.in/docs.</div>
          </div>
          <span class="task-badge badge-tech">tech</span>
        </div>
      </div>
    </div>

    <!-- PHASE 3 -->
    <div class="phase collapsed" id="phase-3">
      <div class="phase-header" onclick="togglePhase('phase-3')">
        <span class="phase-number" style="background:var(--yellow-dim);color:var(--yellow)">P3</span>
        <span class="phase-title">Advanced Features & Growth</span>
        <span class="phase-timeline">Month 3–6</span>
        <span class="phase-progress" id="prog-phase-3" style="color:var(--yellow)">0%</span>
        <span class="phase-toggle">▾</span>
      </div>
      <div class="progress-bar-wrap"><div class="progress-bar-fill" id="bar-phase-3" style="background:var(--yellow);width:0%"></div></div>
      <div class="task-list">
        <div class="task-group-label">Product</div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Subscriptions & recurring billing</div>
            <div class="task-desc">Plan builder, proration, dunning management, customer portal.</div>
          </div>
          <span class="task-badge badge-tech">tech</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Payouts & settlement engine</div>
            <div class="task-desc">NEFT/IMPS/UPI. Daily/weekly/on-demand. Settlement PDF reports.</div>
          </div>
          <span class="task-badge badge-tech">tech</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Split payments / marketplace model</div>
            <div class="task-desc">Route % to sub-accounts. Escrow mode. Razorpay Route integration.</div>
          </div>
          <span class="task-badge badge-tech">tech</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Team management + roles</div>
            <div class="task-desc">Admin / Developer / Viewer. Invite by email. 2FA enforcement.</div>
          </div>
          <span class="task-badge badge-tech">tech</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">@infra-payments/react SDK + InfraCheckout component</div>
            <div class="task-desc">useInfraPayment, useInfraCheckout hooks. Vanilla JS embed script.</div>
          </div>
          <span class="task-badge badge-tech">tech</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Commission engine + GST invoicing</div>
            <div class="task-desc">2% default. Tier logic. 18% GST line item. Monthly PDF invoices via Resend.</div>
          </div>
          <span class="task-badge badge-tech">tech</span>
        </div>
        <div class="task-group-label">Growth</div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Reach 100 active merchants</div>
            <div class="task-desc">Measure: at least 1 live payment in last 30 days.</div>
          </div>
          <span class="task-badge badge-growth">growth</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">₹1Cr GMV milestone</div>
            <div class="task-desc">First major revenue milestone. = ₹2L gross revenue at 2%.</div>
          </div>
          <span class="task-badge badge-growth">growth</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Referral program launch</div>
            <div class="task-desc">Unique codes. 0.1% commission kickback for 12 months. Dashboard tracking.</div>
          </div>
          <span class="task-badge badge-growth">growth</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Partner with 3 dev communities / bootcamps</div>
            <div class="task-desc">iSPIRT, NASSCOM, GDG India, Masai School, Codebasics. Offer free tier.</div>
          </div>
          <span class="task-badge badge-marketing">marketing</span>
        </div>
      </div>
    </div>

    <!-- PHASE 4 -->
    <div class="phase collapsed" id="phase-4">
      <div class="phase-header" onclick="togglePhase('phase-4')">
        <span class="phase-number" style="background:rgba(239,68,68,0.1);color:var(--red)">P4</span>
        <span class="phase-title">Scale & RBI License</span>
        <span class="phase-timeline">Month 6–18</span>
        <span class="phase-progress" id="prog-phase-4" style="color:var(--red)">0%</span>
        <span class="phase-toggle">▾</span>
      </div>
      <div class="progress-bar-wrap"><div class="progress-bar-fill" id="bar-phase-4" style="background:var(--red);width:0%"></div></div>
      <div class="task-list">
        <div class="task-group-label">Regulatory</div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Apply for RBI Payment Aggregator (PA) license</div>
            <div class="task-desc">Requires ₹25Cr net worth. File with RBI DPSS. 12–18 month process.</div>
          </div>
          <span class="task-badge badge-legal">legal</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">PCI DSS Level 1 certification</div>
            <div class="task-desc">Required for PA license. QSA audit. ~₹15–25L cost.</div>
          </div>
          <span class="task-badge badge-legal">legal</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">NPCI membership application (direct UPI access)</div>
            <div class="task-desc">Get off Razorpay's UPI rails. Own UPI handle. Massive margin improvement.</div>
          </div>
          <span class="task-badge badge-legal">legal</span>
        </div>
        <div class="task-group-label">Fundraising</div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Raise pre-seed / seed round ($500K–$2M)</div>
            <div class="task-desc">Target: Lightspeed India, Sequoia Surge, Y Combinator (W/S batch).</div>
          </div>
          <span class="task-badge badge-critical">critical</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Build pitch deck (Sequoia format)</div>
            <div class="task-desc">Problem, market size ($52B global gateway market), traction, team, ask.</div>
          </div>
          <span class="task-badge badge-critical">critical</span>
        </div>
        <div class="task-group-label">Scale Targets</div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">1,000 active merchants</div>
            <div class="task-desc">Paid marketing, content SEO, community. CAC &lt; ₹2,000.</div>
          </div>
          <span class="task-badge badge-growth">growth</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">₹10Cr/month GMV → ₹20L/month gross revenue</div>
            <div class="task-desc">At 2% take rate. Covers ops + team salary at this level.</div>
          </div>
          <span class="task-badge badge-growth">growth</span>
        </div>
        <div class="task" onclick="toggleTask(this)">
          <div class="checkbox"></div>
          <div class="task-content">
            <div class="task-name">Hire first 3 engineers + 1 GTM</div>
            <div class="task-desc">Backend (payments infra), Frontend (DX), DevRel / growth.</div>
          </div>
          <span class="task-badge badge-growth">growth</span>
        </div>
      </div>
    </div>

  </div>

  <!-- NOTES -->
  <div class="notes-section">
    <div class="section-title" style="margin-top:48px">Key Decisions & Context</div>
    <div class="notes-grid">
      <div class="note-card">
        <h4>Revenue Model</h4>
        <ul>
          <li>2% commission on every transaction (Standard)</li>
          <li>1.5% at &gt;₹10L/month GMV (Growth)</li>
          <li>Custom enterprise pricing above ₹1Cr/month</li>
          <li>18% GST added on platform fee — you collect + remit</li>
          <li>Zero setup fees, zero monthly fees</li>
          <li>Referral: 0.1% kickback for 12 months</li>
        </ul>
      </div>
      <div class="note-card">
        <h4>Competitive Moat</h4>
        <ul>
          <li>DX: 5-min setup vs Razorpay's 2-day onboarding</li>
          <li>Brand: Inf₹a = India + infra. Instant recognition.</li>
          <li>Docs: Stripe-quality documentation in India context</li>
          <li>Support: human support from day 1 (vs Razorpay bots)</li>
          <li>Build in public: Twitter following = distribution</li>
          <li>Open-source SDK = developer trust</li>
        </ul>
      </div>
      <div class="note-card">
        <h4>Year 1 Unit Economics</h4>
        <ul>
          <li>Target: 100 merchants × avg ₹5L GMV = ₹5Cr/month GMV</li>
          <li>Gross revenue: ₹10L/month (2%)</li>
          <li>Razorpay cost: ~₹8.5L/month (1.7% to them)</li>
          <li>Net margin: ~₹1.5L/month in year 1</li>
          <li>Break-even: ~50 active merchants at avg ₹5L GMV</li>
          <li>Margin improves dramatically with own PA license</li>
        </ul>
      </div>
      <div class="note-card">
        <h4>Legal Reminders</h4>
        <ul>
          <li>PA license required to hold funds independently</li>
          <li>Year 1: operate as Razorpay reseller (legal, common)</li>
          <li>PCI DSS Level 1 = card data never on Inf₹a servers</li>
          <li>All PII must be stored in India (RBI data localization)</li>
          <li>KYC mandatory: PAN + bank account verification</li>
          <li>PDPB compliance: data deletion on request</li>
        </ul>
      </div>
    </div>
  </div>

  <div class="footer">
    <div class="footer-brand">Inf<span>₹</span>a Technologies Pvt. Ltd. — Internal Command Center</div>
    <div class="last-updated" id="lastUpdated"></div>
  </div>

</div>

<script>
  // Storage key
  const STORAGE_KEY = 'infra_roadmap_v1';

  // Load saved state
  function loadState() {
    try {
      const saved = localStorage.getItem(STORAGE_KEY);
      return saved ? JSON.parse(saved) : { tasks: {}, collapsed: {} };
    } catch(e) { return { tasks: {}, collapsed: {} }; }
  }

  function saveState(state) {
    try { localStorage.setItem(STORAGE_KEY, JSON.stringify(state)); } catch(e) {}
  }

  let state = loadState();

  // Give each task a unique ID
  function initTasks() {
    document.querySelectorAll('.task').forEach((task, i) => {
      if (!task.dataset.id) task.dataset.id = 'task_' + i;
      if (state.tasks[task.dataset.id]) {
        task.classList.add('done');
      }
    });
  }

  function toggleTask(task) {
    const id = task.dataset.id;
    if (task.classList.contains('done')) {
      task.classList.remove('done');
      delete state.tasks[id];
    } else {
      task.classList.add('done');
      state.tasks[id] = true;
    }
    saveState(state);
    updateStats();
    updatePhaseProgress();
    updateTimestamp();
  }

  function togglePhase(phaseId) {
    const phase = document.getElementById(phaseId);
    phase.classList.toggle('collapsed');
    state.collapsed = state.collapsed || {};
    state.collapsed[phaseId] = phase.classList.contains('collapsed');
    saveState(state);
  }

  function restoreCollapsed() {
    if (!state.collapsed) return;
    Object.entries(state.collapsed).forEach(([id, isCollapsed]) => {
      const el = document.getElementById(id);
      if (!el) return;
      if (isCollapsed) el.classList.add('collapsed');
      else el.classList.remove('collapsed');
    });
  }

  function updateStats() {
    const allTasks = document.querySelectorAll('.task');
    const doneTasks = document.querySelectorAll('.task.done');
    const total = allTasks.length;
    const done = doneTasks.length;
    const pct = total > 0 ? Math.round((done/total)*100) : 0;

    document.getElementById('totalCount').textContent = total;
    document.getElementById('doneCount').textContent = done;
    document.getElementById('progressPct').textContent = pct + '%';

    // Current phase = first phase with incomplete tasks
    const phases = ['phase-0','phase-1','phase-2','phase-3','phase-4'];
    let currentPhase = '04';
    for (let i = 0; i < phases.length; i++) {
      const phaseEl = document.getElementById(phases[i]);
      const phaseTasks = phaseEl.querySelectorAll('.task');
      const phaseDone = phaseEl.querySelectorAll('.task.done');
      if (phaseDone.length < phaseTasks.length) {
        currentPhase = '0' + i;
        break;
      }
    }
    document.getElementById('currentPhase').textContent = currentPhase;
  }

  function updatePhaseProgress() {
    const phases = ['phase-0','phase-1','phase-2','phase-3','phase-4'];
    phases.forEach(id => {
      const phaseEl = document.getElementById(id);
      const all = phaseEl.querySelectorAll('.task').length;
      const done = phaseEl.querySelectorAll('.task.done').length;
      const pct = all > 0 ? Math.round((done/all)*100) : 0;
      const progEl = document.getElementById('prog-' + id);
      const barEl = document.getElementById('bar-' + id);
      if (progEl) progEl.textContent = pct + '%';
      if (barEl) barEl.style.width = pct + '%';
    });
  }

  function updateTimestamp() {
    const el = document.getElementById('lastUpdated');
    if (el) {
      const now = new Date();
      el.textContent = 'Last updated ' + now.toLocaleDateString('en-IN', {day:'numeric',month:'short',year:'numeric'}) + ' · ' + now.toLocaleTimeString('en-IN',{hour:'2-digit',minute:'2-digit'});
    }
  }

  function resetAll() {
    if (!confirm('Reset all progress? This cannot be undone.')) return;
    state = { tasks: {}, collapsed: {} };
    saveState(state);
    document.querySelectorAll('.task').forEach(t => t.classList.remove('done'));
    // Re-open all phases
    document.querySelectorAll('.phase').forEach((p, i) => {
      if (i === 0) p.classList.remove('collapsed');
      else p.classList.add('collapsed');
    });
    updateStats();
    updatePhaseProgress();
    updateTimestamp();
  }

  // Init
  initTasks();
  restoreCollapsed();
  updateStats();
  updatePhaseProgress();
  updateTimestamp();
</script>
</body>
</html>
