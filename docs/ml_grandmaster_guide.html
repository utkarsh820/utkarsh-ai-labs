<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ML Grandmaster Playbook</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=JetBrains+Mono:wght@300;400;500&family=Lora:ital,wght@0,400;0,500;1,400&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0a0a0f;
    --surface: #111118;
    --surface2: #16161f;
    --border: #1e1e2e;
    --accent: #f0a500;
    --accent2: #e05a5a;
    --accent3: #5ab4e0;
    --accent4: #5ae0a4;
    --text: #e8e8f0;
    --muted: #888899;
    --code-bg: #0d0d14;
  }
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
  html { scroll-behavior: smooth; }
  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Lora', Georgia, serif;
    font-size: 16px;
    line-height: 1.75;
    overflow-x: hidden;
  }

  /* GRAIN OVERLAY */
  body::before {
    content: '';
    position: fixed; inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none; z-index: 9999; opacity: 0.4;
  }

  /* NAV */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    background: rgba(10,10,15,0.92);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid var(--border);
    display: flex; align-items: center; gap: 0;
    padding: 0 2rem;
    height: 56px;
    overflow-x: auto;
  }
  nav::-webkit-scrollbar { height: 2px; }
  nav::-webkit-scrollbar-thumb { background: var(--accent); }
  .nav-brand {
    font-family: 'Syne', sans-serif;
    font-weight: 800;
    font-size: 1rem;
    color: var(--accent);
    white-space: nowrap;
    margin-right: 2rem;
    letter-spacing: -0.02em;
  }
  .nav-link {
    font-family: 'Syne', sans-serif;
    font-size: 0.72rem;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    color: var(--muted);
    text-decoration: none;
    padding: 0 1rem;
    height: 56px;
    display: flex; align-items: center;
    white-space: nowrap;
    border-bottom: 2px solid transparent;
    transition: color 0.2s, border-color 0.2s;
  }
  .nav-link:hover { color: var(--text); border-color: var(--accent); }
  .nav-link.active { color: var(--accent); border-color: var(--accent); }

  /* HERO */
  .hero {
    padding: 140px 2rem 80px;
    max-width: 900px;
    margin: 0 auto;
    position: relative;
  }
  .hero-tag {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.72rem;
    color: var(--accent);
    letter-spacing: 0.15em;
    text-transform: uppercase;
    margin-bottom: 1.2rem;
    display: flex; align-items: center; gap: 0.5rem;
  }
  .hero-tag::before { content: '//'; opacity: 0.5; }
  h1 {
    font-family: 'Syne', sans-serif;
    font-size: clamp(2.8rem, 6vw, 5rem);
    font-weight: 800;
    line-height: 1.05;
    letter-spacing: -0.03em;
    margin-bottom: 1.5rem;
  }
  h1 span.glow { color: var(--accent); text-shadow: 0 0 40px rgba(240,165,0,0.3); }
  .hero-desc {
    font-size: 1.1rem;
    color: var(--muted);
    max-width: 620px;
    line-height: 1.8;
  }
  .hero-stats {
    display: flex; gap: 2rem; margin-top: 3rem;
    flex-wrap: wrap;
  }
  .stat {
    display: flex; flex-direction: column;
  }
  .stat-num {
    font-family: 'Syne', sans-serif;
    font-size: 2rem;
    font-weight: 800;
    color: var(--accent);
    line-height: 1;
  }
  .stat-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.65rem;
    color: var(--muted);
    text-transform: uppercase;
    letter-spacing: 0.1em;
    margin-top: 0.3rem;
  }

  /* SECTIONS */
  section {
    max-width: 900px;
    margin: 0 auto;
    padding: 80px 2rem;
    border-top: 1px solid var(--border);
  }
  .section-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.68rem;
    color: var(--accent);
    letter-spacing: 0.15em;
    text-transform: uppercase;
    margin-bottom: 0.8rem;
    display: flex; align-items: center; gap: 0.6rem;
  }
  .section-label .num {
    background: var(--accent);
    color: var(--bg);
    padding: 1px 6px;
    font-weight: 700;
    border-radius: 2px;
    font-size: 0.6rem;
  }
  h2 {
    font-family: 'Syne', sans-serif;
    font-size: clamp(1.8rem, 3.5vw, 2.6rem);
    font-weight: 800;
    letter-spacing: -0.02em;
    line-height: 1.15;
    margin-bottom: 1rem;
  }
  h3 {
    font-family: 'Syne', sans-serif;
    font-size: 1.2rem;
    font-weight: 700;
    letter-spacing: -0.01em;
    margin: 2rem 0 0.8rem;
    color: var(--text);
  }
  h4 {
    font-family: 'Syne', sans-serif;
    font-size: 0.95rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.06em;
    color: var(--accent3);
    margin: 1.5rem 0 0.5rem;
  }
  p { margin-bottom: 1rem; color: #ccccd8; }
  strong { color: var(--text); font-weight: 600; }
  em { color: var(--accent); font-style: normal; font-family: 'JetBrains Mono', monospace; font-size: 0.9em; }

  /* CALLOUTS */
  .callout {
    border-left: 3px solid var(--accent);
    background: var(--surface);
    padding: 1rem 1.4rem;
    margin: 1.5rem 0;
    border-radius: 0 6px 6px 0;
  }
  .callout.danger { border-color: var(--accent2); }
  .callout.info { border-color: var(--accent3); }
  .callout.success { border-color: var(--accent4); }
  .callout-title {
    font-family: 'Syne', sans-serif;
    font-size: 0.75rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    margin-bottom: 0.4rem;
  }
  .callout.danger .callout-title { color: var(--accent2); }
  .callout.info .callout-title { color: var(--accent3); }
  .callout.success .callout-title { color: var(--accent4); }
  .callout p { margin: 0; font-size: 0.9rem; }

  /* CODE BLOCKS */
  pre {
    background: var(--code-bg);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 1.2rem 1.4rem;
    overflow-x: auto;
    margin: 1.2rem 0;
    position: relative;
  }
  pre::before {
    content: attr(data-lang);
    position: absolute; top: 8px; right: 12px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.6rem;
    color: var(--muted);
    text-transform: uppercase;
    letter-spacing: 0.1em;
  }
  code {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.82rem;
    line-height: 1.7;
    color: #c8d3f5;
  }
  .c-kw { color: #c099ff; }
  .c-fn { color: #82aaff; }
  .c-st { color: #c3e88d; }
  .c-cm { color: #636da6; font-style: italic; }
  .c-num { color: #f78c6c; }
  .c-var { color: #ffc777; }
  .c-dec { color: #ff98a4; }

  /* TABLES */
  .table-wrap { overflow-x: auto; margin: 1.5rem 0; }
  table {
    width: 100%;
    border-collapse: collapse;
    font-size: 0.85rem;
  }
  th {
    font-family: 'Syne', sans-serif;
    font-size: 0.7rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    color: var(--accent);
    padding: 0.8rem 1rem;
    border-bottom: 2px solid var(--border);
    text-align: left;
    background: var(--surface);
  }
  td {
    padding: 0.7rem 1rem;
    border-bottom: 1px solid var(--border);
    vertical-align: top;
    color: #ccccd8;
  }
  tr:hover td { background: var(--surface); }

  /* DIAGRAM BOXES */
  .diagram {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 1.5rem;
    margin: 1.5rem 0;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.78rem;
    line-height: 2;
    overflow-x: auto;
  }
  .diagram .d-title {
    font-family: 'Syne', sans-serif;
    font-size: 0.7rem;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    color: var(--muted);
    margin-bottom: 1rem;
  }
  .d-row { display: flex; gap: 4px; align-items: center; margin: 3px 0; }
  .d-box {
    padding: 4px 10px;
    border-radius: 4px;
    font-size: 0.7rem;
    font-weight: 500;
    white-space: nowrap;
    text-align: center;
  }
  .d-train { background: rgba(90,180,224,0.15); border: 1px solid rgba(90,180,224,0.4); color: #5ab4e0; }
  .d-val   { background: rgba(240,165,0,0.15);  border: 1px solid rgba(240,165,0,0.4);  color: #f0a500; }
  .d-test  { background: rgba(224,90,90,0.15);  border: 1px solid rgba(224,90,90,0.4);  color: #e05a5a; }
  .d-fold  { background: rgba(90,224,164,0.1);  border: 1px solid rgba(90,224,164,0.3); color: #5ae0a4; }
  .d-arrow { color: var(--muted); font-size: 0.9rem; }
  .d-label { color: var(--muted); font-size: 0.68rem; margin-left: 0.5rem; }

  /* PILL TAGS */
  .tags { display: flex; flex-wrap: wrap; gap: 0.5rem; margin: 1rem 0; }
  .tag {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.65rem;
    padding: 3px 10px;
    border-radius: 20px;
    border: 1px solid;
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }
  .tag-gold   { border-color: var(--accent);  color: var(--accent); }
  .tag-red    { border-color: var(--accent2); color: var(--accent2); }
  .tag-blue   { border-color: var(--accent3); color: var(--accent3); }
  .tag-green  { border-color: var(--accent4); color: var(--accent4); }

  /* GRID CARDS */
  .card-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(240px, 1fr)); gap: 1rem; margin: 1.5rem 0; }
  .card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 1.2rem;
    transition: border-color 0.2s, transform 0.2s;
  }
  .card:hover { border-color: var(--accent); transform: translateY(-2px); }
  .card-icon { font-size: 1.5rem; margin-bottom: 0.6rem; }
  .card-title {
    font-family: 'Syne', sans-serif;
    font-size: 0.9rem;
    font-weight: 700;
    color: var(--text);
    margin-bottom: 0.4rem;
  }
  .card p { font-size: 0.82rem; color: var(--muted); margin: 0; }

  /* STEP LIST */
  .steps { counter-reset: step; list-style: none; margin: 1rem 0; }
  .steps li {
    counter-increment: step;
    display: flex; gap: 1rem;
    margin-bottom: 1.2rem;
    align-items: flex-start;
  }
  .steps li::before {
    content: counter(step);
    min-width: 28px; height: 28px;
    background: var(--accent);
    color: var(--bg);
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-family: 'Syne', sans-serif;
    font-size: 0.75rem;
    font-weight: 800;
    flex-shrink: 0;
    margin-top: 2px;
  }
  .steps li p { margin: 0; font-size: 0.92rem; }

  /* FORMULA */
  .formula {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 1rem 1.5rem;
    margin: 1rem 0;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.85rem;
    color: var(--accent3);
    text-align: center;
  }

  /* PROGRESS/DIFFICULTY */
  .difficulty {
    display: inline-flex; align-items: center; gap: 0.3rem;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.65rem;
    color: var(--muted);
    text-transform: uppercase;
    letter-spacing: 0.05em;
    margin-bottom: 0.5rem;
  }
  .dot { width: 6px; height: 6px; border-radius: 50%; background: var(--border); }
  .dot.on { background: var(--accent); }

  /* TWO COL */
  .two-col { display: grid; grid-template-columns: 1fr 1fr; gap: 1.5rem; margin: 1rem 0; }
  @media (max-width: 600px) { .two-col { grid-template-columns: 1fr; } }

  /* FOOTER */
  footer {
    max-width: 900px;
    margin: 0 auto;
    padding: 3rem 2rem 5rem;
    border-top: 1px solid var(--border);
    color: var(--muted);
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.72rem;
    display: flex; justify-content: space-between; flex-wrap: wrap; gap: 1rem;
  }

  /* SCROLL ANIMATIONS */
  .fade-in { opacity: 0; transform: translateY(20px); transition: opacity 0.6s ease, transform 0.6s ease; }
  .fade-in.visible { opacity: 1; transform: none; }

  /* INLINE CODE */
  code.inline {
    background: var(--surface2);
    border: 1px solid var(--border);
    padding: 1px 6px;
    border-radius: 4px;
    font-size: 0.82em;
    color: #c3e88d;
  }

  .highlight-box {
    background: linear-gradient(135deg, rgba(240,165,0,0.06), rgba(240,165,0,0.02));
    border: 1px solid rgba(240,165,0,0.25);
    border-radius: 10px;
    padding: 1.5rem;
    margin: 1.5rem 0;
  }
  .highlight-box h3 { margin-top: 0; color: var(--accent); }
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <div class="nav-brand">ML Grandmaster</div>
  <a href="#splits" class="nav-link">Dataset Splits</a>
  <a href="#cv" class="nav-link">Cross-Validation</a>
  <a href="#fe" class="nav-link">Feature Engineering</a>
  <a href="#hp" class="nav-link">Hyperparameter Tuning</a>
  <a href="#ensemble" class="nav-link">Ensembles</a>
  <a href="#stacking" class="nav-link">Stacking & Blending</a>
</nav>

<!-- HERO -->
<div class="hero fade-in">
  <div class="hero-tag">Kaggle Grandmaster Playbook · Zero to Elite</div>
  <h1>The Complete<br><span class="glow">ML Grandmaster</span><br>Resource</h1>
  <p class="hero-desc">A first-principles, production-grade, competition-tested guide covering every technique that separates grandmasters from beginners — written for someone starting from zero.</p>
  <div class="hero-stats">
    <div class="stat"><div class="stat-num">6</div><div class="stat-label">Core Pillars</div></div>
    <div class="stat"><div class="stat-num">50+</div><div class="stat-label">Techniques</div></div>
    <div class="stat"><div class="stat-num">30+</div><div class="stat-label">Code Examples</div></div>
    <div class="stat"><div class="stat-num">∞</div><div class="stat-label">Kaggle Gold</div></div>
  </div>
</div>

<!-- ══════════════════════════════════════════
     SECTION 1 — DATASET SPLITS
══════════════════════════════════════════ -->
<section id="splits" class="fade-in">
  <div class="section-label"><span class="num">01</span> Foundation</div>
  <h2>Dataset Splits &amp; Data Leakage</h2>
  <p>Before you train a single model, how you <strong>split your data</strong> determines whether your model actually works in the real world — or whether you've been lying to yourself the entire time. Most beginners lose competitions here.</p>

  <div class="callout danger">
    <div class="callout-title">⚠ The Cardinal Sin: Data Leakage</div>
    <p>Data leakage means your model has seen information it wouldn't have at prediction time. It's the #1 reason models that score perfectly in training fail catastrophically in production and competitions. Everything in this section is designed to prevent it.</p>
  </div>

  <h3>The Three-Way Split</h3>
  <p>Every ML project needs exactly three partitions of your data. Never mix them. Never fit anything on Test.</p>

  <div class="diagram">
    <div class="d-title">Standard Train / Validation / Test Split</div>
    <div class="d-row">
      <div class="d-box d-train" style="flex:7">TRAINING SET (~70%)<br><small>Model learns from this</small></div>
      <div class="d-box d-val" style="flex:1.5">VALIDATION (~15%)<br><small>Tune here</small></div>
      <div class="d-box d-test" style="flex:1.5">TEST (~15%)<br><small>Touch ONCE at end</small></div>
    </div>
    <br>
    <div style="color: var(--muted); font-size: 0.72rem; line-height: 2;">
      ✓ Train: Fit scaler, imputer, encoder, and model<br>
      ✓ Validation: Evaluate, tune hyperparameters, iterate<br>
      ✗ Test: Only use for final evaluation — never for tuning
    </div>
  </div>

  <h4>Why Three Sets?</h4>
  <p><strong>Train</strong> builds the model. <strong>Validation</strong> is used to make decisions about the model (architecture, features, hyperparameters). Once you start making decisions based on validation performance, validation data has "leaked" into your model — so you need a separate <strong>Test set</strong> to get an honest, unbiased estimate of real-world performance.</p>

  <h3>How to Split Correctly</h3>

  <div class="two-col">
    <div class="callout success">
      <div class="callout-title">✓ Random Split (IID Data)</div>
      <p>Use when samples are independent (tabular data, images). Shuffle first, then split. Always set a random seed for reproducibility.</p>
    </div>
    <div class="callout info">
      <div class="callout-title">⚡ Stratified Split (Classification)</div>
      <p>Preserves class distribution in each split. Critical for imbalanced datasets — random split might put all rare class examples in one partition.</p>
    </div>
  </div>

  <div class="two-col">
    <div class="callout info">
      <div class="callout-title">📅 Time-Based Split (Time Series)</div>
      <p>NEVER shuffle time series. Train on past, validate on future. The validation window must chronologically follow training data — no exceptions.</p>
    </div>
    <div class="callout danger">
      <div class="callout-title">👥 Group Split (Dependent Samples)</div>
      <p>If the same entity (user, patient, customer) appears multiple times, all their rows must go into the same split. Group leakage is subtle and devastating.</p>
    </div>
  </div>

<pre data-lang="python"><code><span class="c-kw">from</span> sklearn.model_selection <span class="c-kw">import</span> train_test_split
<span class="c-kw">from</span> sklearn.model_selection <span class="c-kw">import</span> StratifiedShuffleSplit
<span class="c-kw">import</span> pandas <span class="c-kw">as</span> pd

<span class="c-cm"># ── Basic random split ──────────────────────────────────────────</span>
X_trainval, X_test, y_trainval, y_test = train_test_split(
    X, y, test_size=<span class="c-num">0.15</span>, random_state=<span class="c-num">42</span>
)
X_train, X_val, y_train, y_val = train_test_split(
    X_trainval, y_trainval, test_size=<span class="c-num">0.176</span>,  <span class="c-cm"># 15% of original</span>
    random_state=<span class="c-num">42</span>
)

<span class="c-cm"># ── Stratified split (classification) ───────────────────────────</span>
X_train, X_val, y_train, y_val = train_test_split(
    X, y, test_size=<span class="c-num">0.2</span>, stratify=y, random_state=<span class="c-num">42</span>
)

<span class="c-cm"># ── Time-series split ───────────────────────────────────────────</span>
df = df.sort_values(<span class="c-st">'date'</span>)
cutoff = <span class="c-kw">int</span>(<span class="c-kw">len</span>(df) * <span class="c-num">0.8</span>)
train_df = df.iloc[:cutoff]
test_df  = df.iloc[cutoff:]

<span class="c-cm"># ── Group split ─────────────────────────────────────────────────</span>
<span class="c-kw">from</span> sklearn.model_selection <span class="c-kw">import</span> GroupShuffleSplit
gss = GroupShuffleSplit(n_splits=<span class="c-num">1</span>, test_size=<span class="c-num">0.2</span>, random_state=<span class="c-num">42</span>)
train_idx, val_idx = <span class="c-kw">next</span>(gss.split(X, y, groups=df[<span class="c-st">'user_id'</span>]))</code></pre>

  <h3>The 12 Forms of Data Leakage</h3>
  <div class="table-wrap">
    <table>
      <tr><th>Leakage Type</th><th>What Goes Wrong</th><th>Fix</th></tr>
      <tr><td><strong>Feature leakage</strong></td><td>Feature encodes the label (e.g., "is_fraud" column in fraud detection)</td><td>Remove target-correlated features found only after event</td></tr>
      <tr><td><strong>Temporal leakage</strong></td><td>Using future data to predict the past (e.g., next-day price to predict today)</td><td>Strict time-ordered splits; lag all features</td></tr>
      <tr><td><strong>Preprocessing leakage</strong></td><td>Fitting scaler/imputer on full dataset before splitting</td><td>Always fit preprocessing ONLY on train set</td></tr>
      <tr><td><strong>Duplicate leakage</strong></td><td>Same row in both train and test</td><td>Deduplicate before splitting</td></tr>
      <tr><td><strong>Group leakage</strong></td><td>Same user/entity in train and test</td><td>Use GroupKFold; split by group</td></tr>
      <tr><td><strong>Lookahead bias</strong></td><td>Target encoding computed on full train without CV</td><td>Use out-of-fold target encoding</td></tr>
      <tr><td><strong>Proxy leakage</strong></td><td>A feature indirectly encodes the label</td><td>Domain knowledge + correlation analysis</td></tr>
      <tr><td><strong>ID leakage</strong></td><td>Row index or ID predicts the label in competitions</td><td>Always investigate IDs and sequential patterns</td></tr>
    </table>
  </div>

  <div class="callout success">
    <div class="callout-title">✓ Grandmaster Checklist for Splits</div>
    <p>① Sort by time if temporal data · ② Check for duplicates before splitting · ③ Check group membership (users/customers) · ④ Fit ALL transformers only on train · ⑤ Test set is sacred — never tune on it · ⑥ Your validation score must mirror the leaderboard — if not, your split is wrong</p>
  </div>
</section>

<!-- ══════════════════════════════════════════
     SECTION 2 — CROSS-VALIDATION
══════════════════════════════════════════ -->
<section id="cv" class="fade-in">
  <div class="section-label"><span class="num">02</span> Model Evaluation</div>
  <h2>Cross-Validation</h2>
  <p>Cross-validation (CV) is the art of getting a <strong>reliable, unbiased estimate</strong> of your model's generalization performance without wasting data. Grandmasters obsess over CV because <em>if your CV doesn't correlate with the leaderboard, you're flying blind</em>.</p>

  <h3>Why Simple Train/Val Isn't Enough</h3>
  <p>A single validation split gives you a noisy estimate. You got lucky (or unlucky) with which 20% became the validation set. With K-Fold CV, you use every sample for validation exactly once, averaging K estimates — far more reliable.</p>

  <h3>K-Fold Cross-Validation</h3>
  <p>Split data into K equal folds. Train on K-1, validate on 1. Repeat K times. Average the K scores.</p>

  <div class="diagram">
    <div class="d-title">5-Fold Cross-Validation</div>
    <div class="d-row"><div class="d-box d-fold">Fold 1 → VAL</div><div class="d-box d-train" style="flex:4">Fold 2 · 3 · 4 · 5  →  TRAIN</div><div class="d-label">Score₁</div></div>
    <div class="d-row"><div class="d-box d-train">Fold 1</div><div class="d-box d-fold">Fold 2 → VAL</div><div class="d-box d-train" style="flex:3">Fold 3 · 4 · 5  →  TRAIN</div><div class="d-label">Score₂</div></div>
    <div class="d-row"><div class="d-box d-train" style="flex:2">Fold 1 · 2</div><div class="d-box d-fold">Fold 3 → VAL</div><div class="d-box d-train" style="flex:2">Fold 4 · 5  →  TRAIN</div><div class="d-label">Score₃</div></div>
    <div class="d-row"><div class="d-box d-train" style="flex:3">Fold 1 · 2 · 3</div><div class="d-box d-fold">Fold 4 → VAL</div><div class="d-box d-train">Fold 5</div><div class="d-label">Score₄</div></div>
    <div class="d-row"><div class="d-box d-train" style="flex:4">Fold 1 · 2 · 3 · 4  →  TRAIN</div><div class="d-box d-fold">Fold 5 → VAL</div><div class="d-label">Score₅</div></div>
    <br>
    <div style="color: var(--accent); font-size: 0.75rem;">Final CV Score = mean(Score₁…Score₅) ± std(Score₁…Score₅)</div>
  </div>

<pre data-lang="python"><code><span class="c-kw">from</span> sklearn.model_selection <span class="c-kw">import</span> KFold, StratifiedKFold, cross_val_score
<span class="c-kw">import</span> numpy <span class="c-kw">as</span> np

<span class="c-cm"># ── Standard K-Fold ─────────────────────────────────────────────</span>
kf = KFold(n_splits=<span class="c-num">5</span>, shuffle=<span class="c-kw">True</span>, random_state=<span class="c-num">42</span>)
scores = cross_val_score(model, X, y, cv=kf, scoring=<span class="c-st">'rmse'</span>)
<span class="c-fn">print</span>(<span class="c-st">f"CV: </span>{np.mean(scores):.4f}<span class="c-st"> ± </span>{np.std(scores):.4f}<span class="c-st">"</span>)

<span class="c-cm"># ── Stratified K-Fold (ALWAYS use for classification) ────────────</span>
skf = StratifiedKFold(n_splits=<span class="c-num">5</span>, shuffle=<span class="c-kw">True</span>, random_state=<span class="c-num">42</span>)

<span class="c-cm"># ── Manual CV loop (more control — grandmaster style) ────────────</span>
oof_preds = np.zeros(<span class="c-kw">len</span>(X))   <span class="c-cm"># out-of-fold predictions</span>
test_preds = np.zeros(<span class="c-kw">len</span>(X_test))

<span class="c-kw">for</span> fold, (train_idx, val_idx) <span class="c-kw">in</span> <span class="c-fn">enumerate</span>(skf.split(X, y)):
    X_tr, X_vl = X[train_idx], X[val_idx]
    y_tr, y_vl = y[train_idx], y[val_idx]
    
    model.fit(X_tr, y_tr)
    oof_preds[val_idx] = model.predict_proba(X_vl)[:, <span class="c-num">1</span>]
    test_preds += model.predict_proba(X_test)[:, <span class="c-num">1</span>] / <span class="c-num">5</span>

<span class="c-cm"># OOF AUC — your TRUE model performance estimate</span>
<span class="c-kw">from</span> sklearn.metrics <span class="c-kw">import</span> roc_auc_score
oof_score = roc_auc_score(y, oof_preds)
<span class="c-fn">print</span>(<span class="c-st">f"OOF AUC: </span>{oof_score:.5f}<span class="c-st">"</span>)</code></pre>

  <h3>All CV Strategies — When to Use Each</h3>
  <div class="table-wrap">
    <table>
      <tr><th>Strategy</th><th>Use Case</th><th>Kaggle Use</th><th>Key Param</th></tr>
      <tr><td><strong>KFold</strong></td><td>Regression, balanced data</td><td>Very common</td><td>n_splits=5 or 10</td></tr>
      <tr><td><strong>StratifiedKFold</strong></td><td>Classification</td><td>Most common for clf</td><td>n_splits=5</td></tr>
      <tr><td><strong>GroupKFold</strong></td><td>Repeated entities (users, patients)</td><td>Critical for correct CV</td><td>groups=entity_col</td></tr>
      <tr><td><strong>TimeSeriesSplit</strong></td><td>Time series forecasting</td><td>Only for temporal data</td><td>n_splits=5, gap</td></tr>
      <tr><td><strong>StratifiedGroupKFold</strong></td><td>Groups + class imbalance</td><td>Medical, NLP comps</td><td>groups + stratify</td></tr>
      <tr><td><strong>RepeatedKFold</strong></td><td>Small datasets, high variance</td><td>Low-data competitions</td><td>n_repeats=3–10</td></tr>
      <tr><td><strong>LeaveOneOut (LOO)</strong></td><td>Very tiny datasets (&lt;100 rows)</td><td>Rarely</td><td>—</td></tr>
      <tr><td><strong>Nested CV</strong></td><td>Unbiased HPO + evaluation together</td><td>Research / robustness</td><td>outer + inner</td></tr>
    </table>
  </div>

  <h3>Time Series Cross-Validation</h3>
  <div class="diagram">
    <div class="d-title">Time Series Split — Expanding Window</div>
    <div class="d-row"><div class="d-box d-train" style="width:80px">Jan</div><div class="d-box d-fold" style="width:60px">Feb →</div><div class="d-label">Score₁</div></div>
    <div class="d-row"><div class="d-box d-train" style="width:130px">Jan · Feb</div><div class="d-box d-fold" style="width:60px">Mar →</div><div class="d-label">Score₂</div></div>
    <div class="d-row"><div class="d-box d-train" style="width:180px">Jan · Feb · Mar</div><div class="d-box d-fold" style="width:60px">Apr →</div><div class="d-label">Score₃</div></div>
    <div class="d-row"><div class="d-box d-train" style="width:230px">Jan · Feb · Mar · Apr</div><div class="d-box d-fold" style="width:60px">May →</div><div class="d-label">Score₄</div></div>
    <div style="margin-top:0.8rem; color: var(--muted); font-size: 0.72rem;">⚠ Always add a GAP between train and validation to simulate real deployment lag</div>
  </div>

<pre data-lang="python"><code><span class="c-kw">from</span> sklearn.model_selection <span class="c-kw">import</span> TimeSeriesSplit

tscv = TimeSeriesSplit(n_splits=<span class="c-num">5</span>, gap=<span class="c-num">7</span>)  <span class="c-cm"># gap=7 day buffer</span>

<span class="c-kw">for</span> train_idx, val_idx <span class="c-kw">in</span> tscv.split(X):
    X_tr, X_vl = X.iloc[train_idx], X.iloc[val_idx]
    y_tr, y_vl = y.iloc[train_idx], y.iloc[val_idx]
    model.fit(X_tr, y_tr)
    score = model.score(X_vl, y_vl)
    <span class="c-fn">print</span>(<span class="c-st">f"Fold score: </span>{score:.4f}<span class="c-st">"</span>)</code></pre>

  <h3>Nested Cross-Validation</h3>
  <p>When you want to <strong>tune hyperparameters AND get an unbiased performance estimate</strong>, you need nested CV. Without it, your performance estimate is optimistically biased because you used the same data to select hyperparameters and evaluate the model.</p>

  <div class="diagram">
    <div class="d-title">Nested CV: Outer loop evaluates, Inner loop tunes</div>
    <div style="color: #ccccd8; font-size: 0.75rem; line-height: 2.2;">
      OUTER FOLD 1: [Train+Val] ──► Inner 5-Fold CV to find best HPs ──► Evaluate on Outer Test → Score₁<br>
      OUTER FOLD 2: [Train+Val] ──► Inner 5-Fold CV to find best HPs ──► Evaluate on Outer Test → Score₂<br>
      OUTER FOLD 3: [Train+Val] ──► Inner 5-Fold CV to find best HPs ──► Evaluate on Outer Test → Score₃<br>
      <br>
      <span style="color: var(--accent);">Final Score = mean(Score₁, Score₂, Score₃)  ← Honest. Unbiased.</span>
    </div>
  </div>

<pre data-lang="python"><code><span class="c-kw">from</span> sklearn.model_selection <span class="c-kw">import</span> GridSearchCV, cross_val_score, KFold
<span class="c-kw">from</span> sklearn.ensemble <span class="c-kw">import</span> RandomForestClassifier

outer_cv = KFold(n_splits=<span class="c-num">5</span>, shuffle=<span class="c-kw">True</span>, random_state=<span class="c-num">42</span>)
inner_cv = KFold(n_splits=<span class="c-num">3</span>, shuffle=<span class="c-kw">True</span>, random_state=<span class="c-num">0</span>)

param_grid = {<span class="c-st">'n_estimators'</span>: [<span class="c-num">100</span>, <span class="c-num">200</span>], <span class="c-st">'max_depth'</span>: [<span class="c-num">5</span>, <span class="c-num">10</span>, <span class="c-kw">None</span>]}
model = RandomForestClassifier(random_state=<span class="c-num">42</span>)

<span class="c-cm"># GridSearchCV acts as the inner CV loop</span>
clf = GridSearchCV(model, param_grid, cv=inner_cv, scoring=<span class="c-st">'roc_auc'</span>)

<span class="c-cm"># Outer loop gives unbiased performance estimate</span>
nested_scores = cross_val_score(clf, X, y, cv=outer_cv, scoring=<span class="c-st">'roc_auc'</span>)
<span class="c-fn">print</span>(<span class="c-st">f"Nested CV AUC: </span>{nested_scores.mean():.4f}<span class="c-st"> ± </span>{nested_scores.std():.4f}<span class="c-st">"</span>)</code></pre>

  <div class="callout success">
    <div class="callout-title">✓ Grandmaster CV Wisdom</div>
    <p>① Always track OOF (out-of-fold) predictions — they're gold for stacking · ② If CV std is high relative to mean, your model is unstable · ③ In competitions, your CV must track the public leaderboard within 0.001 — if it doesn't, your split is wrong · ④ Use the same CV folds everywhere to ensure fair model comparisons · ⑤ For time series, always include a gap between train and validation</p>
  </div>
</section>

<!-- ══════════════════════════════════════════
     SECTION 3 — FEATURE ENGINEERING
══════════════════════════════════════════ -->
<section id="fe" class="fade-in">
  <div class="section-label"><span class="num">03</span> Data Craftsmanship</div>
  <h2>Feature Engineering</h2>
  <p>Feature engineering is the process of using domain knowledge and mathematical creativity to <strong>transform raw data into representations that make patterns easier for models to learn</strong>. It is the single biggest competitive differentiator in Kaggle. Great features beat great algorithms almost every time.</p>

  <div class="callout">
    <div class="callout-title">💡 The Grandmaster Mindset</div>
    <p>"Give the model what it needs to know, in the form it can best understand." Every feature should answer a question about the data. Bad features are noise — they hurt. Feature engineering is not blind generation; it's thoughtful construction.</p>
  </div>

  <h3>1. Handling Missing Values</h3>
  <p>Missing data is information. Don't blindly impute — think about <em>why</em> the data is missing.</p>

<pre data-lang="python"><code><span class="c-kw">import</span> pandas <span class="c-kw">as</span> pd
<span class="c-kw">import</span> numpy <span class="c-kw">as</span> np
<span class="c-kw">from</span> sklearn.impute <span class="c-kw">import</span> SimpleImputer, KNNImputer

<span class="c-cm"># ── Always create a "was missing" flag first ─────────────────────</span>
df[<span class="c-st">'age_was_missing'</span>] = df[<span class="c-st">'age'</span>].isna().astype(int)

<span class="c-cm"># ── Numeric imputation strategies ───────────────────────────────</span>
df[<span class="c-st">'age_median'</span>]     = df[<span class="c-st">'age'</span>].fillna(df[<span class="c-st">'age'</span>].median())     <span class="c-cm"># robust to outliers</span>
df[<span class="c-st">'age_mean'</span>]       = df[<span class="c-st">'age'</span>].fillna(df[<span class="c-st">'age'</span>].mean())       <span class="c-cm"># assumes normality</span>
df[<span class="c-st">'age_group_med'</span>]  = df.groupby(<span class="c-st">'gender'</span>)[<span class="c-st">'age'</span>].transform(<span class="c-st">'median'</span>)  <span class="c-cm"># group-aware</span>

<span class="c-cm"># ── KNN imputation (captures correlations) ───────────────────────</span>
knn_imp = KNNImputer(n_neighbors=<span class="c-num">5</span>)
X_imputed = knn_imp.fit_transform(X_train)  <span class="c-cm"># fit on train only!</span>

<span class="c-cm"># ── Categorical imputation ───────────────────────────────────────</span>
df[<span class="c-st">'cat'</span>].fillna(<span class="c-st">'MISSING'</span>, inplace=<span class="c-kw">True</span>)  <span class="c-cm"># treat as category</span>
df[<span class="c-st">'cat'</span>].fillna(df[<span class="c-st">'cat'</span>].mode()[<span class="c-num">0</span>])         <span class="c-cm"># most frequent</span></code></pre>

  <h3>2. Categorical Encoding</h3>
  <p>Models can't handle strings — you must convert categories to numbers. The choice of encoding has massive impact on model performance.</p>

  <div class="table-wrap">
    <table>
      <tr><th>Encoding</th><th>When to Use</th><th>Pros / Cons</th></tr>
      <tr><td><strong>Label Encoding</strong></td><td>Ordinal categories (small, medium, large)</td><td>Simple; implies false ordering for nominal cats</td></tr>
      <tr><td><strong>One-Hot Encoding</strong></td><td>Nominal, low cardinality (&lt;20 values)</td><td>No ordering assumption; explodes with high cardinality</td></tr>
      <tr><td><strong>Target Encoding</strong></td><td>High-cardinality nominal features</td><td>Powerful; leaks if not done inside CV</td></tr>
      <tr><td><strong>Frequency/Count Enc.</strong></td><td>Any categorical, competition default</td><td>No leakage; captures popularity signal</td></tr>
      <tr><td><strong>Binary Encoding</strong></td><td>High cardinality with tree models</td><td>Compact; good for trees</td></tr>
      <tr><td><strong>Ordinal Encoding</strong></td><td>Tree-based models, any categorical</td><td>Trees split categories; no explosion</td></tr>
      <tr><td><strong>Embeddings</strong></td><td>Very high cardinality (100k+ values), NLP</td><td>Best quality; needs neural net training</td></tr>
    </table>
  </div>

<pre data-lang="python"><code><span class="c-kw">import</span> pandas <span class="c-kw">as</span> pd
<span class="c-kw">from</span> category_encoders <span class="c-kw">import</span> TargetEncoder, BinaryEncoder

<span class="c-cm"># ── One-Hot Encoding ────────────────────────────────────────────</span>
df = pd.get_dummies(df, columns=[<span class="c-st">'city'</span>], drop_first=<span class="c-kw">True</span>)

<span class="c-cm"># ── Frequency Encoding (safe, no leakage) ───────────────────────</span>
freq_map = df[<span class="c-st">'city'</span>].value_counts(normalize=<span class="c-kw">True</span>)
df[<span class="c-st">'city_freq'</span>] = df[<span class="c-st">'city'</span>].map(freq_map)

<span class="c-cm"># ── Target Encoding INSIDE CV (CRITICAL — avoids leakage) ────────</span>
oof_target_enc = np.zeros(<span class="c-kw">len</span>(train))

<span class="c-kw">for</span> train_idx, val_idx <span class="c-kw">in</span> kf.split(train):
    enc = TargetEncoder(smoothing=<span class="c-num">10</span>)  <span class="c-cm"># smoothing prevents overfitting</span>
    enc.fit(train.iloc[train_idx][<span class="c-st">'city'</span>], y[train_idx])
    oof_target_enc[val_idx] = enc.transform(
        train.iloc[val_idx][<span class="c-st">'city'</span>]
    ).values.flatten()

<span class="c-cm"># ── Leave-One-Out Target Encoding (grandmaster technique) ─────────</span>
<span class="c-kw">def</span> <span class="c-fn">loo_target_encode</span>(df, col, target, smoothing=<span class="c-num">10</span>):
    means = df.groupby(col)[target].mean()
    global_mean = df[target].mean()
    counts = df.groupby(col)[target].count()
    smooth = <span class="c-num">1</span> / (<span class="c-num">1</span> + np.exp(-(counts - <span class="c-num">1</span>) / smoothing))
    <span class="c-kw">return</span> df[col].map(smooth * means + (<span class="c-num">1</span> - smooth) * global_mean)</code></pre>

  <h3>3. Numerical Transformations</h3>

<pre data-lang="python"><code><span class="c-kw">import</span> numpy <span class="c-kw">as</span> np
<span class="c-kw">from</span> sklearn.preprocessing <span class="c-kw">import</span> StandardScaler, RobustScaler, PowerTransformer

<span class="c-cm"># ── Scaling (ONLY fit on train) ──────────────────────────────────</span>
scaler = RobustScaler()          <span class="c-cm"># handles outliers better than StandardScaler</span>
X_train = scaler.fit_transform(X_train)
X_test  = scaler.transform(X_test)   <span class="c-cm"># ← transform only, never fit!</span>

<span class="c-cm"># ── Log transforms (fix right-skewed distributions) ──────────────</span>
df[<span class="c-st">'log_price'</span>]    = np.log1p(df[<span class="c-st">'price'</span>])     <span class="c-cm"># log1p handles zeros</span>
df[<span class="c-st">'sqrt_count'</span>]   = np.sqrt(df[<span class="c-st">'count'</span>])

<span class="c-cm"># ── Box-Cox / Yeo-Johnson (make distribution Gaussian) ────────────</span>
pt = PowerTransformer(method=<span class="c-st">'yeo-johnson'</span>)  <span class="c-cm"># handles negatives unlike Box-Cox</span>
df_transformed = pt.fit_transform(df[[<span class="c-st">'price'</span>, <span class="c-st">'age'</span>]])

<span class="c-cm"># ── Clipping outliers ────────────────────────────────────────────</span>
lower = df[<span class="c-st">'salary'</span>].quantile(<span class="c-num">0.01</span>)
upper = df[<span class="c-st">'salary'</span>].quantile(<span class="c-num">0.99</span>)
df[<span class="c-st">'salary_clipped'</span>] = df[<span class="c-st">'salary'</span>].clip(lower, upper)

<span class="c-cm"># ── Binning / Discretization ─────────────────────────────────────</span>
df[<span class="c-st">'age_bin'</span>] = pd.cut(df[<span class="c-st">'age'</span>], bins=[<span class="c-num">0</span>,<span class="c-num">18</span>,<span class="c-num">35</span>,<span class="c-num">55</span>,<span class="c-num">100</span>], labels=[<span class="c-num">0</span>,<span class="c-num">1</span>,<span class="c-num">2</span>,<span class="c-num">3</span>])
df[<span class="c-st">'age_qbin'</span>] = pd.qcut(df[<span class="c-st">'age'</span>], q=<span class="c-num">4</span>, labels=<span class="c-kw">False</span>)  <span class="c-cm"># equal-frequency bins</span></code></pre>

  <h3>4. Feature Creation — The Creative Part</h3>

<pre data-lang="python"><code><span class="c-cm"># ── Interaction features ─────────────────────────────────────────</span>
df[<span class="c-st">'bmi'</span>]          = df[<span class="c-st">'weight'</span>] / (df[<span class="c-st">'height'</span>] ** <span class="c-num">2</span>)
df[<span class="c-st">'price_per_sqft'</span>] = df[<span class="c-st">'price'</span>] / df[<span class="c-st">'sqft'</span>].replace(<span class="c-num">0</span>, np.nan)
df[<span class="c-st">'age_income'</span>]    = df[<span class="c-st">'age'</span>] * df[<span class="c-st">'income'</span>]   <span class="c-cm"># multiplicative interaction</span>

<span class="c-cm"># ── Polynomial features (use carefully — dimensionality explodes) ──</span>
<span class="c-kw">from</span> sklearn.preprocessing <span class="c-kw">import</span> PolynomialFeatures
poly = PolynomialFeatures(degree=<span class="c-num">2</span>, interaction_only=<span class="c-kw">True</span>, include_bias=<span class="c-kw">False</span>)
X_poly = poly.fit_transform(X)

<span class="c-cm"># ── Aggregation features (group-level statistics) ────────────────</span>
agg = df.groupby(<span class="c-st">'user_id'</span>).agg(
    n_purchases     = (<span class="c-st">'amount'</span>, <span class="c-st">'count'</span>),
    total_spend     = (<span class="c-st">'amount'</span>, <span class="c-st">'sum'</span>),
    avg_spend       = (<span class="c-st">'amount'</span>, <span class="c-st">'mean'</span>),
    max_spend       = (<span class="c-st">'amount'</span>, <span class="c-st">'max'</span>),
    spend_std       = (<span class="c-st">'amount'</span>, <span class="c-st">'std'</span>),
    unique_products = (<span class="c-st">'product_id'</span>, <span class="c-st">'nunique'</span>)
).reset_index()
df = df.merge(agg, on=<span class="c-st">'user_id'</span>, how=<span class="c-st">'left'</span>)

<span class="c-cm"># ── Datetime features (rich signal source) ───────────────────────</span>
df[<span class="c-st">'ts'</span>] = pd.to_datetime(df[<span class="c-st">'timestamp'</span>])
df[<span class="c-st">'hour'</span>]         = df[<span class="c-st">'ts'</span>].dt.hour
df[<span class="c-st">'day_of_week'</span>]  = df[<span class="c-st">'ts'</span>].dt.dayofweek
df[<span class="c-st">'is_weekend'</span>]   = (df[<span class="c-st">'day_of_week'</span>] &gt;= <span class="c-num">5</span>).astype(int)
df[<span class="c-st">'month'</span>]        = df[<span class="c-st">'ts'</span>].dt.month
df[<span class="c-st">'quarter'</span>]      = df[<span class="c-st">'ts'</span>].dt.quarter
df[<span class="c-st">'days_since'</span>]   = (pd.Timestamp.now() - df[<span class="c-st">'ts'</span>]).dt.days

<span class="c-cm"># ── Cyclical encoding (hour, month, day — wrap around) ────────────</span>
df[<span class="c-st">'hour_sin'</span>] = np.sin(<span class="c-num">2</span> * np.pi * df[<span class="c-st">'hour'</span>] / <span class="c-num">24</span>)
df[<span class="c-st">'hour_cos'</span>] = np.cos(<span class="c-num">2</span> * np.pi * df[<span class="c-st">'hour'</span>] / <span class="c-num">24</span>)

<span class="c-cm"># ── Lag features (time series) ────────────────────────────────────</span>
df = df.sort_values([<span class="c-st">'user_id'</span>, <span class="c-st">'date'</span>])
<span class="c-kw">for</span> lag <span class="c-kw">in</span> [<span class="c-num">1</span>, <span class="c-num">7</span>, <span class="c-num">14</span>, <span class="c-num">30</span>]:
    df[<span class="c-st">f'sales_lag_</span>{lag}<span class="c-st">'</span>] = df.groupby(<span class="c-st">'user_id'</span>)[<span class="c-st">'sales'</span>].shift(lag)

<span class="c-cm"># ── Rolling window features ───────────────────────────────────────</span>
df[<span class="c-st">'sales_roll7_mean'</span>] = df.groupby(<span class="c-st">'user_id'</span>)[<span class="c-st">'sales'</span>].transform(
    <span class="c-kw">lambda</span> x: x.shift(<span class="c-num">1</span>).rolling(<span class="c-num">7</span>).mean()   <span class="c-cm"># shift(1) avoids leakage</span>
)</code></pre>

  <h3>5. Feature Selection</h3>
  <p>More features is NOT always better. Irrelevant features add noise, slow training, and can hurt performance — especially in linear models.</p>

<pre data-lang="python"><code><span class="c-kw">import</span> lightgbm <span class="c-kw">as</span> lgb

<span class="c-cm"># ── Feature importance from tree models ──────────────────────────</span>
model = lgb.LGBMClassifier()
model.fit(X_train, y_train)
importances = pd.Series(model.feature_importances_, index=X_train.columns)
top_features = importances.nlargest(<span class="c-num">30</span>).index.tolist()

<span class="c-cm"># ── SHAP values (gold standard) ───────────────────────────────────</span>
<span class="c-kw">import</span> shap
explainer = shap.TreeExplainer(model)
shap_values = explainer.shap_values(X_val)
shap.summary_plot(shap_values, X_val)

<span class="c-cm"># ── Variance threshold (remove near-constant features) ───────────</span>
<span class="c-kw">from</span> sklearn.feature_selection <span class="c-kw">import</span> VarianceThreshold
selector = VarianceThreshold(threshold=<span class="c-num">0.01</span>)
X_filtered = selector.fit_transform(X_train)

<span class="c-cm"># ── Correlation filter (remove redundant features) ────────────────</span>
corr_matrix = pd.DataFrame(X_train).corr().abs()
upper = corr_matrix.where(np.triu(np.ones(corr_matrix.shape), k=<span class="c-num">1</span>).astype(bool))
to_drop = [col <span class="c-kw">for</span> col <span class="c-kw">in</span> upper.columns <span class="c-kw">if</span> any(upper[col] &gt; <span class="c-num">0.95</span>)]

<span class="c-cm"># ── Recursive Feature Elimination with CV ────────────────────────</span>
<span class="c-kw">from</span> sklearn.feature_selection <span class="c-kw">import</span> RFECV
rfecv = RFECV(estimator=model, cv=<span class="c-num">5</span>, scoring=<span class="c-st">'roc_auc'</span>, min_features_to_select=<span class="c-num">10</span>)
rfecv.fit(X_train, y_train)</code></pre>

  <div class="callout success">
    <div class="callout-title">✓ Feature Engineering Grandmaster Tips</div>
    <p>① Never generate features blindly — understand what each feature represents · ② Always validate new features with CV before keeping them · ③ Target encode only inside CV loops · ④ Shift time series features by at least 1 period to avoid leakage · ⑤ SHAP values are your best friend for debugging feature importance · ⑥ Interaction features often beat raw features in competitions · ⑦ Group aggregation features (user-level stats) are extremely powerful in tabular competitions</p>
  </div>
</section>

<!-- ══════════════════════════════════════════
     SECTION 4 — HYPERPARAMETER TUNING
══════════════════════════════════════════ -->
<section id="hp" class="fade-in">
  <div class="section-label"><span class="num">04</span> Model Optimization</div>
  <h2>Hyperparameter Tuning</h2>
  <p>Hyperparameters are settings you choose before training that <strong>control how the model learns</strong>. Unlike model parameters (weights), hyperparameters are not learned from data. Tuning them properly can yield 1–5% performance gains that matter enormously in competition.</p>

  <h3>The Tuning Landscape</h3>
  <div class="card-grid">
    <div class="card">
      <div class="card-icon">🔲</div>
      <div class="card-title">Grid Search</div>
      <p>Exhaustively tries every combination. Thorough but exponentially slow. Use only for &lt;3 params with small grids.</p>
    </div>
    <div class="card">
      <div class="card-icon">🎲</div>
      <div class="card-title">Random Search</div>
      <p>Randomly samples the space. Surprisingly effective — often finds good solutions with 20x fewer trials than Grid Search.</p>
    </div>
    <div class="card">
      <div class="card-icon">🧠</div>
      <div class="card-title">Bayesian Optimization</div>
      <p>Builds a probabilistic model of the objective function. Tries smarter points. Best for expensive evaluations.</p>
    </div>
    <div class="card">
      <div class="card-icon">✂️</div>
      <div class="card-title">Successive Halving</div>
      <p>Runs many candidates briefly, keeps the best half, repeats. Extremely fast — the modern default.</p>
    </div>
  </div>

<pre data-lang="python"><code><span class="c-kw">from</span> sklearn.model_selection <span class="c-kw">import</span> GridSearchCV, RandomizedSearchCV
<span class="c-kw">from</span> sklearn.experimental <span class="c-kw">import</span> enable_halving_search_cv
<span class="c-kw">from</span> sklearn.model_selection <span class="c-kw">import</span> HalvingRandomSearchCV
<span class="c-kw">from</span> scipy.stats <span class="c-kw">import</span> randint, uniform, loguniform
<span class="c-kw">import</span> xgboost <span class="c-kw">as</span> xgb

<span class="c-cm"># ── Grid Search (use for small, discrete param spaces) ────────────</span>
grid = {<span class="c-st">'max_depth'</span>: [<span class="c-num">3</span>,<span class="c-num">5</span>,<span class="c-num">7</span>], <span class="c-st">'learning_rate'</span>: [<span class="c-num">0.01</span>, <span class="c-num">0.1</span>]}
gs = GridSearchCV(xgb.XGBClassifier(), grid, cv=<span class="c-num">5</span>, scoring=<span class="c-st">'roc_auc'</span>, n_jobs=<span class="c-num">-1</span>)
gs.fit(X_train, y_train)
<span class="c-fn">print</span>(gs.best_params_, gs.best_score_)

<span class="c-cm"># ── Random Search (use as default starting point) ─────────────────</span>
param_dist = {
    <span class="c-st">'n_estimators'</span>     : randint(<span class="c-num">100</span>, <span class="c-num">1000</span>),
    <span class="c-st">'max_depth'</span>        : randint(<span class="c-num">3</span>, <span class="c-num">12</span>),
    <span class="c-st">'learning_rate'</span>    : loguniform(<span class="c-num">1e-4</span>, <span class="c-num">0.3</span>),
    <span class="c-st">'subsample'</span>        : uniform(<span class="c-num">0.5</span>, <span class="c-num">0.5</span>),
    <span class="c-st">'colsample_bytree'</span> : uniform(<span class="c-num">0.5</span>, <span class="c-num">0.5</span>),
    <span class="c-st">'min_child_weight'</span> : randint(<span class="c-num">1</span>, <span class="c-num">10</span>),
    <span class="c-st">'reg_alpha'</span>        : loguniform(<span class="c-num">1e-5</span>, <span class="c-num">10</span>),
    <span class="c-st">'reg_lambda'</span>       : loguniform(<span class="c-num">1e-5</span>, <span class="c-num">10</span>),
}
rs = RandomizedSearchCV(
    xgb.XGBClassifier(), param_dist,
    n_iter=<span class="c-num">100</span>, cv=<span class="c-num">5</span>, scoring=<span class="c-st">'roc_auc'</span>,
    n_jobs=<span class="c-num">-1</span>, random_state=<span class="c-num">42</span>
)
rs.fit(X_train, y_train)</code></pre>

  <h3>Optuna — The Grandmaster Standard</h3>
  <p>Optuna is the go-to hyperparameter optimization framework in modern Kaggle. It implements Tree-structured Parzen Estimator (TPE) — a Bayesian algorithm that learns from previous trials to make smarter suggestions.</p>

<pre data-lang="python"><code><span class="c-kw">import</span> optuna
optuna.logging.set_verbosity(optuna.logging.WARNING)  <span class="c-cm"># quiet</span>

<span class="c-kw">def</span> <span class="c-fn">objective</span>(trial):
    params = {
        <span class="c-st">'n_estimators'</span>     : trial.suggest_int(<span class="c-st">'n_estimators'</span>, <span class="c-num">200</span>, <span class="c-num">2000</span>),
        <span class="c-st">'max_depth'</span>        : trial.suggest_int(<span class="c-st">'max_depth'</span>, <span class="c-num">3</span>, <span class="c-num">12</span>),
        <span class="c-st">'learning_rate'</span>    : trial.suggest_float(<span class="c-st">'learning_rate'</span>, <span class="c-num">1e-4</span>, <span class="c-num">0.3</span>, log=<span class="c-kw">True</span>),
        <span class="c-st">'subsample'</span>        : trial.suggest_float(<span class="c-st">'subsample'</span>, <span class="c-num">0.5</span>, <span class="c-num">1.0</span>),
        <span class="c-st">'colsample_bytree'</span> : trial.suggest_float(<span class="c-st">'colsample_bytree'</span>, <span class="c-num">0.5</span>, <span class="c-num">1.0</span>),
        <span class="c-st">'min_child_weight'</span> : trial.suggest_int(<span class="c-st">'min_child_weight'</span>, <span class="c-num">1</span>, <span class="c-num">20</span>),
        <span class="c-st">'reg_alpha'</span>        : trial.suggest_float(<span class="c-st">'reg_alpha'</span>, <span class="c-num">1e-8</span>, <span class="c-num">10</span>, log=<span class="c-kw">True</span>),
        <span class="c-st">'reg_lambda'</span>       : trial.suggest_float(<span class="c-st">'reg_lambda'</span>, <span class="c-num">1e-8</span>, <span class="c-num">10</span>, log=<span class="c-kw">True</span>),
        <span class="c-st">'gamma'</span>            : trial.suggest_float(<span class="c-st">'gamma'</span>, <span class="c-num">0</span>, <span class="c-num">5</span>),
        <span class="c-st">'tree_method'</span>      : <span class="c-st">'hist'</span>,
        <span class="c-st">'eval_metric'</span>      : <span class="c-st">'auc'</span>,
        <span class="c-st">'use_label_encoder'</span>: <span class="c-kw">False</span>,
    }
    
    model = xgb.XGBClassifier(**params)
    cv_score = cross_val_score(
        model, X_train, y_train, cv=<span class="c-num">5</span>, scoring=<span class="c-st">'roc_auc'</span>
    ).mean()
    <span class="c-kw">return</span> cv_score   <span class="c-cm"># Optuna maximizes this</span>

study = optuna.create_study(direction=<span class="c-st">'maximize'</span>)
study.optimize(objective, n_trials=<span class="c-num">200</span>, timeout=<span class="c-num">3600</span>)  <span class="c-cm"># 200 trials or 1hr</span>

<span class="c-fn">print</span>(<span class="c-st">"Best Score:"</span>, study.best_value)
<span class="c-fn">print</span>(<span class="c-st">"Best Params:"</span>, study.best_params)

<span class="c-cm"># Visualize optimization history</span>
optuna.visualization.plot_optimization_history(study)
optuna.visualization.plot_param_importances(study)</code></pre>

  <h3>LightGBM with Early Stopping — The Fast Grandmaster Way</h3>
  <p>For gradient boosting models, <strong>early stopping</strong> removes the need to tune <code class="inline">n_estimators</code> manually — just set it large and let the model stop when it stops improving.</p>

<pre data-lang="python"><code><span class="c-kw">import</span> lightgbm <span class="c-kw">as</span> lgb

params = {
    <span class="c-st">'learning_rate'</span>   : <span class="c-num">0.05</span>,
    <span class="c-st">'num_leaves'</span>      : <span class="c-num">127</span>,
    <span class="c-st">'max_depth'</span>       : <span class="c-num">-1</span>,
    <span class="c-st">'feature_fraction'</span>: <span class="c-num">0.7</span>,
    <span class="c-st">'bagging_fraction'</span>: <span class="c-num">0.7</span>,
    <span class="c-st">'bagging_freq'</span>    : <span class="c-num">5</span>,
    <span class="c-st">'reg_alpha'</span>       : <span class="c-num">0.1</span>,
    <span class="c-st">'reg_lambda'</span>      : <span class="c-num">0.1</span>,
    <span class="c-st">'objective'</span>       : <span class="c-st">'binary'</span>,
    <span class="c-st">'metric'</span>          : <span class="c-st">'auc'</span>,
    <span class="c-st">'verbosity'</span>       : <span class="c-num">-1</span>,
}

dtrain = lgb.Dataset(X_train, label=y_train)
dval   = lgb.Dataset(X_val,   label=y_val, reference=dtrain)

model = lgb.train(
    params, dtrain,
    num_boost_round     = <span class="c-num">10000</span>,
    valid_sets          = [dval],
    callbacks           = [
        lgb.early_stopping(stopping_rounds=<span class="c-num">100</span>),  <span class="c-cm"># stop if no improvement</span>
        lgb.log_evaluation(period=<span class="c-num">200</span>),
    ],
)
<span class="c-fn">print</span>(<span class="c-st">f"Best iteration: </span>{model.best_iteration}<span class="c-st">"</span>)
<span class="c-fn">print</span>(<span class="c-st">f"Best AUC: </span>{model.best_score[<span class="c-st">'valid_0'</span>][<span class="c-st">'auc'</span>]:.5f}<span class="c-st">"</span>)</code></pre>

  <h3>XGBoost, LightGBM, CatBoost — Key Hyperparameters</h3>
  <div class="table-wrap">
    <table>
      <tr><th>Parameter</th><th>What It Controls</th><th>Typical Range</th><th>Effect</th></tr>
      <tr><td><code class="inline">learning_rate</code></td><td>Step size per tree</td><td>0.01–0.3</td><td>Lower = more trees needed, better generalization</td></tr>
      <tr><td><code class="inline">max_depth</code></td><td>Tree depth (XGB/LGBM)</td><td>3–12</td><td>Deeper = more complex = more overfit</td></tr>
      <tr><td><code class="inline">num_leaves</code></td><td>Max leaves per tree (LGBM)</td><td>15–500</td><td>LGBM's primary complexity control</td></tr>
      <tr><td><code class="inline">subsample</code></td><td>Row sampling per tree</td><td>0.5–1.0</td><td>Lower = more regularization</td></tr>
      <tr><td><code class="inline">colsample_bytree</code></td><td>Feature sampling per tree</td><td>0.5–1.0</td><td>Lower = more regularization</td></tr>
      <tr><td><code class="inline">min_child_weight</code></td><td>Min samples per leaf</td><td>1–20</td><td>Higher = less overfit</td></tr>
      <tr><td><code class="inline">reg_alpha / reg_lambda</code></td><td>L1 / L2 regularization</td><td>0–10</td><td>Higher = more regularization</td></tr>
      <tr><td><code class="inline">n_estimators</code></td><td>Number of trees</td><td>Set large + early stopping</td><td>More = better, up to early stop point</td></tr>
    </table>
  </div>

  <div class="callout success">
    <div class="callout-title">✓ HPO Grandmaster Strategy</div>
    <p>① Use Optuna with TPE sampler as your default · ② First coarse-search a wide range, then fine-tune the best region · ③ Always use CV inside the objective function — never tune on a single split · ④ Use early stopping to remove n_estimators from the search space · ⑤ Lower learning_rate + more trees almost always helps at the end · ⑥ Log-uniform sampling for learning_rate and regularization — they span orders of magnitude</p>
  </div>
</section>

<!-- ══════════════════════════════════════════
     SECTION 5 — ENSEMBLES
══════════════════════════════════════════ -->
<section id="ensemble" class="fade-in">
  <div class="section-label"><span class="num">05</span> Model Combinations</div>
  <h2>Ensemble Methods</h2>
  <p>No single model wins Kaggle. <strong>Ensembles combine multiple models to get predictions better than any single model</strong>. This is not a trick — it's backed by the bias-variance decomposition. Diverse models make different errors, and averaging those errors out is mathematically powerful.</p>

  <div class="formula">Ensemble Error = Bias² + Variance/n + Irreducible Noise/n</div>
  <p style="text-align:center; font-size:0.85rem; color: var(--muted);">Averaging n uncorrelated models reduces variance by a factor of n.</p>

  <h3>The Three Families</h3>
  <div class="card-grid">
    <div class="card">
      <div class="card-icon">🎒</div>
      <div class="card-title">Bagging</div>
      <p>Train models on bootstrap samples of the data. Reduces <strong>variance</strong>. Models are independent. Classic: Random Forest.</p>
    </div>
    <div class="card">
      <div class="card-icon">📈</div>
      <div class="card-title">Boosting</div>
      <p>Train models sequentially. Each learns from the errors of the previous. Reduces <strong>bias</strong>. Classic: XGBoost, LightGBM, CatBoost.</p>
    </div>
    <div class="card">
      <div class="card-icon">🗳️</div>
      <div class="card-title">Voting / Averaging</div>
      <p>Combine predictions from diverse, independently trained models. Simple but often very powerful in competition.</p>
    </div>
  </div>

  <h3>Bagging Deep Dive</h3>
  <p>Bagging trains K models on K bootstrap samples (sampling with replacement). Because each model sees different data, they make different errors. Averaging reduces variance without changing bias.</p>

<pre data-lang="python"><code><span class="c-kw">from</span> sklearn.ensemble <span class="c-kw">import</span> BaggingClassifier, RandomForestClassifier
<span class="c-kw">from</span> sklearn.tree <span class="c-kw">import</span> DecisionTreeClassifier

<span class="c-cm"># ── Manual bagging to understand it ─────────────────────────────</span>
preds = []
<span class="c-kw">for</span> i <span class="c-kw">in</span> <span class="c-fn">range</span>(<span class="c-num">100</span>):
    bootstrap_idx = np.random.choice(<span class="c-kw">len</span>(X_train), <span class="c-kw">len</span>(X_train), replace=<span class="c-kw">True</span>)
    X_boot, y_boot = X_train[bootstrap_idx], y_train[bootstrap_idx]
    m = DecisionTreeClassifier(max_depth=<span class="c-num">10</span>).fit(X_boot, y_boot)
    preds.append(m.predict_proba(X_val)[:, <span class="c-num">1</span>])
final = np.mean(preds, axis=<span class="c-num">0</span>)

<span class="c-cm"># ── Random Forest = Bagging + Feature Subsampling ────────────────</span>
rf = RandomForestClassifier(
    n_estimators   = <span class="c-num">500</span>,
    max_features   = <span class="c-st">'sqrt'</span>,    <span class="c-cm"># sqrt(n_features) per split</span>
    max_depth      = <span class="c-kw">None</span>,
    min_samples_leaf = <span class="c-num">1</span>,
    n_jobs         = <span class="c-num">-1</span>,
    random_state   = <span class="c-num">42</span>,
    oob_score      = <span class="c-kw">True</span>,     <span class="c-cm"># free validation using out-of-bag samples</span>
).fit(X_train, y_train)

<span class="c-fn">print</span>(<span class="c-st">f"OOB Score: </span>{rf.oob_score_:.5f}<span class="c-st">"</span>)  <span class="c-cm"># equivalent to CV score, free!</span></code></pre>

  <h3>Gradient Boosting Deep Dive</h3>
  <p>Boosting fits models <em>sequentially</em>. Each new tree fits the <strong>residuals</strong> (errors) of all previous trees. The learning rate controls how much each tree contributes.</p>

  <div class="diagram">
    <div class="d-title">Gradient Boosting — Sequential Error Correction</div>
    <div style="font-family: 'JetBrains Mono', monospace; font-size: 0.75rem; color: #ccccd8; line-height: 2.3;">
      Initial prediction: <span style="color: var(--accent);">F₀(x) = mean(y)</span><br>
      Compute residuals: <span style="color: var(--accent3);">r₁ = y - F₀(x)</span><br>
      Train tree on residuals: <span style="color: var(--accent4);">h₁(x)</span><br>
      Update: <span style="color: var(--accent);">F₁(x) = F₀(x) + η·h₁(x)</span><br>
      Compute new residuals: <span style="color: var(--accent3);">r₂ = y - F₁(x)</span><br>
      Train tree on residuals: <span style="color: var(--accent4);">h₂(x)</span><br>
      Update: <span style="color: var(--accent);">F₂(x) = F₁(x) + η·h₂(x)</span><br>
      ... repeat T times ...<br>
      Final: <span style="color: var(--accent);">F_T(x) = F₀(x) + η·Σhₜ(x)</span>
    </div>
  </div>

<pre data-lang="python"><code><span class="c-kw">import</span> lightgbm <span class="c-kw">as</span> lgb
<span class="c-kw">import</span> xgboost <span class="c-kw">as</span> xgb
<span class="c-kw">import</span> catboost <span class="c-kw">as</span> cb

<span class="c-cm"># ── LightGBM (fastest, great for tabular) ────────────────────────</span>
lgbm = lgb.LGBMClassifier(
    n_estimators   = <span class="c-num">5000</span>,
    learning_rate  = <span class="c-num">0.03</span>,
    num_leaves     = <span class="c-num">127</span>,
    feature_fraction = <span class="c-num">0.7</span>,
    bagging_fraction = <span class="c-num">0.8</span>,
    bagging_freq   = <span class="c-num">5</span>,
    reg_alpha      = <span class="c-num">0.1</span>, reg_lambda = <span class="c-num">1.0</span>,
    random_state   = <span class="c-num">42</span>,
)

<span class="c-cm"># ── XGBoost (very reliable, great HPO ecosystem) ─────────────────</span>
xgbm = xgb.XGBClassifier(
    n_estimators   = <span class="c-num">5000</span>,
    learning_rate  = <span class="c-num">0.03</span>,
    max_depth      = <span class="c-num">6</span>,
    subsample      = <span class="c-num">0.8</span>,
    colsample_bytree = <span class="c-num">0.8</span>,
    use_label_encoder = <span class="c-kw">False</span>,
    eval_metric    = <span class="c-st">'auc'</span>,
    tree_method    = <span class="c-st">'hist'</span>,  <span class="c-cm"># GPU: 'gpu_hist'</span>
    random_state   = <span class="c-num">42</span>,
)

<span class="c-cm"># ── CatBoost (best for categoricals — no encoding needed!) ────────</span>
catb = cb.CatBoostClassifier(
    iterations     = <span class="c-num">5000</span>,
    learning_rate  = <span class="c-num">0.03</span>,
    depth          = <span class="c-num">6</span>,
    cat_features   = cat_feature_indices,  <span class="c-cm"># pass categorical indices</span>
    eval_metric    = <span class="c-st">'AUC'</span>,
    random_seed    = <span class="c-num">42</span>,
    verbose        = <span class="c-num">200</span>,
)

<span class="c-cm"># ── Simple Averaging Ensemble ────────────────────────────────────</span>
lgbm.fit(X_train, y_train)
xgbm.fit(X_train, y_train)
catb.fit(X_train, y_train)

p1 = lgbm.predict_proba(X_test)[:, <span class="c-num">1</span>]
p2 = xgbm.predict_proba(X_test)[:, <span class="c-num">1</span>]
p3 = catb.predict_proba(X_test)[:, <span class="c-num">1</span>]

ensemble = (p1 + p2 + p3) / <span class="c-num">3</span>       <span class="c-cm"># simple average</span>
ensemble = <span class="c-num">0.4</span>*p1 + <span class="c-num">0.35</span>*p2 + <span class="c-num">0.25</span>*p3  <span class="c-cm"># weighted average</span></code></pre>

  <h3>Voting Ensembles</h3>

<pre data-lang="python"><code><span class="c-kw">from</span> sklearn.ensemble <span class="c-kw">import</span> VotingClassifier, VotingRegressor

<span class="c-cm"># ── Hard voting (majority vote — not recommended for Kaggle) ──────</span>
<span class="c-cm"># ── Soft voting (average probabilities — USE THIS) ────────────────</span>
voting_clf = VotingClassifier(
    estimators=[
        (<span class="c-st">'lgbm'</span>, lgbm),
        (<span class="c-st">'xgb'</span>,  xgbm),
        (<span class="c-st">'cat'</span>,  catb),
    ],
    voting=<span class="c-st">'soft'</span>,   <span class="c-cm"># use predicted probabilities, not class labels</span>
    weights=[<span class="c-num">2</span>, <span class="c-num">1.5</span>, <span class="c-num">1</span>],  <span class="c-cm"># weight by CV score</span>
)
voting_clf.fit(X_train, y_train)</code></pre>

  <div class="callout">
    <div class="callout-title">🏆 The Diversity Principle</div>
    <p>Ensembles only help when models are <strong>diverse</strong>. Averaging two nearly identical LightGBM models barely helps. Averaging LightGBM + XGBoost + a Neural Network + a Linear Model gives massive gains because they make different errors. Correlation between model errors is the enemy of ensembling.</p>
  </div>
</section>

<!-- ══════════════════════════════════════════
     SECTION 6 — STACKING & BLENDING
══════════════════════════════════════════ -->
<section id="stacking" class="fade-in">
  <div class="section-label"><span class="num">06</span> Elite Techniques</div>
  <h2>Stacking &amp; Blending</h2>
  <p>Stacking and blending are <strong>meta-learning techniques</strong> — you train a second model (the meta-learner) to optimally combine the predictions of your first-level models. This is how every winning Kaggle solution works at the top.</p>

  <h3>Stacking Architecture</h3>

  <div class="diagram">
    <div class="d-title">2-Level Stacking Architecture</div>
    <div style="font-family: 'JetBrains Mono', monospace; font-size: 0.74rem; color: #ccccd8; line-height: 2.2;">
      <span style="color: var(--muted);">LEVEL 0 (Base Models) — trained on original features:</span><br>
      &nbsp;&nbsp;[LightGBM] [XGBoost] [CatBoost] [Neural Net] [Linear Model]<br>
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↓ OOF predictions on train / averaged predictions on test<br>
      <span style="color: var(--muted);">LEVEL 1 (Meta-Learner) — trained on base model predictions:</span><br>
      &nbsp;&nbsp;Input: [lgbm_pred, xgb_pred, cat_pred, nn_pred, lr_pred]<br>
      &nbsp;&nbsp;Model: Logistic Regression / Ridge / LightGBM<br>
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↓<br>
      <span style="color: var(--accent);">FINAL PREDICTION</span>
    </div>
  </div>

  <div class="callout danger">
    <div class="callout-title">⚠ The Stacking Leakage Trap</div>
    <p>If you train base models on all training data, then use their predictions to train the meta-learner on the same data — you have catastrophic leakage. Base models have "memorized" the training data, so their predictions perfectly encode the labels. Solution: Out-of-Fold (OOF) predictions.</p>
  </div>

  <h3>Out-of-Fold Stacking — The Correct Way</h3>

<pre data-lang="python"><code><span class="c-kw">import</span> numpy <span class="c-kw">as</span> np
<span class="c-kw">from</span> sklearn.model_selection <span class="c-kw">import</span> StratifiedKFold
<span class="c-kw">from</span> sklearn.linear_model <span class="c-kw">import</span> LogisticRegression, Ridge
<span class="c-kw">import</span> lightgbm <span class="c-kw">as</span> lgb
<span class="c-kw">import</span> xgboost <span class="c-kw">as</span> xgb

<span class="c-kw">def</span> <span class="c-fn">get_oof_predictions</span>(model, X_train, y_train, X_test, n_folds=<span class="c-num">5</span>):
    <span class="c-st">"""
    Train model using K-Fold CV.
    Returns:
      oof_preds  — shape (n_train,): train predictions with NO leakage
      test_preds — shape (n_test,):  averaged predictions on test
    """</span>
    kf = StratifiedKFold(n_splits=n_folds, shuffle=<span class="c-kw">True</span>, random_state=<span class="c-num">42</span>)
    oof_preds   = np.zeros(<span class="c-kw">len</span>(X_train))
    test_preds  = np.zeros(<span class="c-kw">len</span>(X_test))

    <span class="c-kw">for</span> fold, (tr_idx, vl_idx) <span class="c-kw">in</span> <span class="c-fn">enumerate</span>(kf.split(X_train, y_train)):
        X_tr, X_vl = X_train[tr_idx], X_train[vl_idx]
        y_tr, y_vl = y_train[tr_idx], y_train[vl_idx]

        model.fit(X_tr, y_tr)

        oof_preds[vl_idx] = model.predict_proba(X_vl)[:, <span class="c-num">1</span>]
        test_preds        += model.predict_proba(X_test)[:, <span class="c-num">1</span>] / n_folds

    oof_score = roc_auc_score(y_train, oof_preds)
    <span class="c-fn">print</span>(<span class="c-st">f"OOF AUC: </span>{oof_score:.5f}<span class="c-st">"</span>)
    <span class="c-kw">return</span> oof_preds, test_preds


<span class="c-cm"># ═══ LEVEL 0: Generate OOF predictions for each base model ════════</span>
lgbm_oof, lgbm_test = <span class="c-fn">get_oof_predictions</span>(
    lgb.LGBMClassifier(n_estimators=<span class="c-num">500</span>, random_state=<span class="c-num">42</span>),
    X_train, y_train, X_test
)
xgb_oof, xgb_test = <span class="c-fn">get_oof_predictions</span>(
    xgb.XGBClassifier(n_estimators=<span class="c-num">500</span>, use_label_encoder=<span class="c-kw">False</span>),
    X_train, y_train, X_test
)
lr_oof, lr_test = <span class="c-fn">get_oof_predictions</span>(
    LogisticRegression(C=<span class="c-num">0.1</span>, max_iter=<span class="c-num">1000</span>),
    X_train, y_train, X_test
)

<span class="c-cm"># ═══ LEVEL 1: Build meta-feature matrix ═══════════════════════════</span>
meta_train = np.column_stack([lgbm_oof, xgb_oof, lr_oof])   <span class="c-cm"># shape: (n_train, 3)</span>
meta_test  = np.column_stack([lgbm_test, xgb_test, lr_test]) <span class="c-cm"># shape: (n_test, 3)</span>

<span class="c-cm"># You can also add original features to the meta learner!</span>
meta_train_aug = np.hstack([meta_train, X_train])
meta_test_aug  = np.hstack([meta_test,  X_test])

<span class="c-cm"># ═══ LEVEL 1: Train meta-learner ═════════════════════════════════</span>
<span class="c-cm"># Use a simple, regularized model to avoid overfitting meta-features</span>
meta_model = LogisticRegression(C=<span class="c-num">0.1</span>)       <span class="c-cm"># simple for stacking</span>
meta_model.fit(meta_train, y_train)

final_preds = meta_model.predict_proba(meta_test)[:, <span class="c-num">1</span>]
<span class="c-fn">print</span>(<span class="c-st">f"Stack weights: </span>{meta_model.coef_}<span class="c-st">"</span>)</code></pre>

  <h3>Blending — Simpler, Faster, Still Powerful</h3>
  <p>Blending is a simplified stacking where you use a <strong>held-out validation set</strong> (not OOF) to train the meta-learner. Faster to implement, slightly more biased, but widely used in practice.</p>

  <div class="two-col">
    <div class="callout info">
      <div class="callout-title">📊 Stacking vs Blending</div>
      <p><strong>Stacking:</strong> Uses ALL training data via OOF. More data efficient. Preferred for small datasets. More complex to implement. Standard in serious competitions.</p>
    </div>
    <div class="callout">
      <div class="callout-title">⚡ When to Use Blending</div>
      <p><strong>Blending:</strong> Uses a holdout set. Simpler, faster. Slight data waste. Fine for large datasets (&gt;50k rows). Easier to add new models quickly.</p>
    </div>
  </div>

<pre data-lang="python"><code><span class="c-cm"># ═══ BLENDING PIPELINE ═══════════════════════════════════════════</span>
<span class="c-cm"># Split training data into blend_train and blend_val</span>
X_btrain, X_bval, y_btrain, y_bval = train_test_split(
    X_train, y_train, test_size=<span class="c-num">0.2</span>, random_state=<span class="c-num">42</span>, stratify=y_train
)

models = {
    <span class="c-st">'lgbm'</span>: lgb.LGBMClassifier(n_estimators=<span class="c-num">500</span>),
    <span class="c-st">'xgb'</span> : xgb.XGBClassifier(n_estimators=<span class="c-num">500</span>),
    <span class="c-st">'cat'</span> : cb.CatBoostClassifier(iterations=<span class="c-num">500</span>, verbose=<span class="c-num">0</span>),
}

blend_train = np.zeros((<span class="c-kw">len</span>(X_bval), <span class="c-kw">len</span>(models)))
blend_test  = np.zeros((<span class="c-kw">len</span>(X_test),  <span class="c-kw">len</span>(models)))

<span class="c-kw">for</span> i, (name, m) <span class="c-kw">in</span> <span class="c-fn">enumerate</span>(models.items()):
    m.fit(X_btrain, y_btrain)                               <span class="c-cm"># train on blend_train</span>
    blend_train[:, i] = m.predict_proba(X_bval)[:, <span class="c-num">1</span>]     <span class="c-cm"># predict blend_val</span>
    blend_test[:, i]  = m.predict_proba(X_test)[:, <span class="c-num">1</span>]     <span class="c-cm"># predict test</span>

<span class="c-cm"># Train meta-learner on blend_val predictions</span>
meta = LogisticRegression(C=<span class="c-num">1.0</span>)
meta.fit(blend_train, y_bval)
final_preds = meta.predict_proba(blend_test)[:, <span class="c-num">1</span>]</code></pre>

  <h3>Advanced: Multi-Level Stacking</h3>
<pre data-lang="python"><code><span class="c-cm"># Level 0: Diverse base models → generate OOF features</span>
<span class="c-cm"># Level 1: Mid-level learners (e.g., another LightGBM) trained on L0 OOF</span>
<span class="c-cm"># Level 2: Meta-learner (e.g., Ridge) trained on L1 OOF</span>

<span class="c-cm"># The key rule: each level must use OOF to avoid leakage</span>
<span class="c-cm"># In practice, 2 levels is almost always sufficient</span>
<span class="c-cm"># 3+ levels rarely helps and risks overfitting the meta-features</span>

<span class="c-cm"># ── sklearn's built-in StackingClassifier ────────────────────────</span>
<span class="c-kw">from</span> sklearn.ensemble <span class="c-kw">import</span> StackingClassifier

stack = StackingClassifier(
    estimators=[
        (<span class="c-st">'lgbm'</span>, lgb.LGBMClassifier(n_estimators=<span class="c-num">500</span>)),
        (<span class="c-st">'xgb'</span>,  xgb.XGBClassifier(n_estimators=<span class="c-num">500</span>)),
        (<span class="c-st">'rf'</span>,   RandomForestClassifier(n_estimators=<span class="c-num">300</span>)),
    ],
    final_estimator=LogisticRegression(C=<span class="c-num">0.1</span>),
    cv=<span class="c-num">5</span>,          <span class="c-cm"># OOF automatically handled</span>
    stack_method=<span class="c-st">'predict_proba'</span>,
    passthrough=<span class="c-kw">True</span>,   <span class="c-cm"># also pass original features to meta-learner</span>
    n_jobs=<span class="c-num">-1</span>
)
stack.fit(X_train, y_train)</code></pre>

  <h3>Optimal Blending Weights — Finding Them Scientifically</h3>

<pre data-lang="python"><code><span class="c-kw">from</span> scipy.optimize <span class="c-kw">import</span> minimize
<span class="c-kw">from</span> sklearn.metrics <span class="c-kw">import</span> roc_auc_score

<span class="c-cm"># Assume oof1, oof2, oof3 are OOF predictions from 3 models</span>
oof_preds = np.column_stack([lgbm_oof, xgb_oof, cat_oof])  <span class="c-cm"># (n, 3)</span>

<span class="c-kw">def</span> <span class="c-fn">neg_auc</span>(weights):
    weights = np.array(weights)
    weights /= weights.sum()   <span class="c-cm"># normalize to sum to 1</span>
    blend = (oof_preds * weights).sum(axis=<span class="c-num">1</span>)
    <span class="c-kw">return</span> -roc_auc_score(y_train, blend)

<span class="c-cm"># Optimize weights using Nelder-Mead</span>
result = minimize(
    neg_auc,
    x0=[<span class="c-num">1</span>/<span class="c-num">3</span>, <span class="c-num">1</span>/<span class="c-num">3</span>, <span class="c-num">1</span>/<span class="c-num">3</span>],  <span class="c-cm"># start equal</span>
    method=<span class="c-st">'Nelder-Mead'</span>,
    options={<span class="c-st">'maxiter'</span>: <span class="c-num">1000</span>}
)
best_weights = result.x / result.x.sum()
<span class="c-fn">print</span>(<span class="c-st">f"Optimal weights: </span>{best_weights}<span class="c-st">"</span>)

<span class="c-cm"># Apply to test set</span>
test_preds_matrix = np.column_stack([lgbm_test, xgb_test, cat_test])
final = (test_preds_matrix * best_weights).sum(axis=<span class="c-num">1</span>)</code></pre>

  <h3>Complete Grandmaster Pipeline</h3>
  <div class="highlight-box">
    <h3>🏆 The Winning Competition Blueprint</h3>
    <ol class="steps">
      <li><p><strong>Understand the metric</strong> and build a validation setup that mirrors it perfectly. Your CV must track the leaderboard.</p></li>
      <li><p><strong>Build a solid baseline</strong> — simple LightGBM with default params, clean features. Get on the board.</p></li>
      <li><p><strong>Invest heavily in feature engineering</strong> — aggregate features, interaction terms, target encoding (inside CV), datetime features, lag features.</p></li>
      <li><p><strong>Tune hyperparameters</strong> with Optuna after feature engineering is stable. Use early stopping. Lock learning rate last.</p></li>
      <li><p><strong>Build diverse base models</strong> — LightGBM + XGBoost + CatBoost + Neural Net + Linear Model. Collect OOF predictions from all of them.</p></li>
      <li><p><strong>Stack or blend</strong> — use OOF predictions as meta-features. Train a simple meta-learner (Ridge or Logistic Regression). Add original features to meta-learner.</p></li>
      <li><p><strong>Optimize blend weights</strong> using Nelder-Mead or Optuna on OOF predictions against the target metric.</p></li>
      <li><p><strong>Pseudo-labeling</strong> (advanced) — predict test set with high confidence, add to training, retrain base models.</p></li>
    </ol>
  </div>

  <div class="callout success">
    <div class="callout-title">✓ Final Grandmaster Wisdom</div>
    <p>① The meta-learner should be <em>simple</em> — Ridge, Lasso, Logistic Regression. Complex meta-learners overfit the small meta-feature matrix. · ② Correlation between base model predictions = wasted ensemble capacity. Maximize diversity. · ③ Neural networks + gradient boosting together almost always outperform either alone. · ④ Always validate your ensemble with OOF — if your stacking OOF score is worse than your best base model, something is wrong. · ⑤ "Shake-up" in competitions happens when your CV doesn't match the LB — fix your validation first, always.</p>
  </div>

  <h3>Quick Reference Summary</h3>
  <div class="table-wrap">
    <table>
      <tr><th>Technique</th><th>When to Use</th><th>Gain Potential</th><th>Complexity</th></tr>
      <tr><td><strong>K-Fold CV</strong></td><td>Always — reliable score estimation</td><td>N/A (evaluation tool)</td><td>Low</td></tr>
      <tr><td><strong>Stratified KFold</strong></td><td>Classification tasks</td><td>N/A</td><td>Low</td></tr>
      <tr><td><strong>TimeSeriesSplit</strong></td><td>Any temporal data</td><td>N/A</td><td>Low</td></tr>
      <tr><td><strong>Target Encoding</strong></td><td>High-cardinality categoricals</td><td>+0.5–2%</td><td>Medium</td></tr>
      <tr><td><strong>Feature Interactions</strong></td><td>When domain knowledge suggests</td><td>+0.3–1%</td><td>Medium</td></tr>
      <tr><td><strong>Lag/Rolling Features</strong></td><td>Time series</td><td>+1–5%</td><td>Medium</td></tr>
      <tr><td><strong>Bayesian HPO (Optuna)</strong></td><td>After features are stable</td><td>+0.5–2%</td><td>Medium</td></tr>
      <tr><td><strong>Averaging (XGB+LGB+CB)</strong></td><td>Final submission</td><td>+0.3–1%</td><td>Low</td></tr>
      <tr><td><strong>Stacking</strong></td><td>Top 10 competition push</td><td>+0.5–2%</td><td>High</td></tr>
      <tr><td><strong>Multi-Level Stacking</strong></td><td>Top 3 competition push</td><td>+0.1–0.5%</td><td>Very High</td></tr>
    </table>
  </div>
</section>

<footer>
  <div>ML Grandmaster Playbook · Cross-Validation · Feature Engineering · HPO · Ensembles · Stacking</div>
  <div>Built for Kaggle Grandmaster Track</div>
</footer>

<script>
  // Scroll animations
  const els = document.querySelectorAll('.fade-in');
  const obs = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) { e.target.classList.add('visible'); obs.unobserve(e.target); }
    });
  }, { threshold: 0.05 });
  els.forEach(el => obs.observe(el));

  // Active nav
  const sections = document.querySelectorAll('section[id]');
  const navLinks = document.querySelectorAll('.nav-link');
  const navObs = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        navLinks.forEach(l => l.classList.remove('active'));
        const active = document.querySelector(`.nav-link[href="#${e.target.id}"]`);
        if (active) active.classList.add('active');
      }
    });
  }, { threshold: 0.3 });
  sections.forEach(s => navObs.observe(s));
</script>
</body>
</html>
