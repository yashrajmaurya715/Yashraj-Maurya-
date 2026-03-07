<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Yashraj — AI Developer & Vibe Coder</title>
  <link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@400;600;800&display=swap" rel="stylesheet"/>
  <style>
    *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

    :root {
      --bg: #050810;
      --bg2: #090d1a;
      --card: #0d1226;
      --accent: #00f5d4;
      --accent2: #7b61ff;
      --accent3: #ff6b6b;
      --text: #e8eaf6;
      --muted: #6b7280;
      --border: rgba(0,245,212,0.12);
    }

    html { scroll-behavior: smooth; }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: 'Syne', sans-serif;
      overflow-x: hidden;
    }

    /* NOISE OVERLAY */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.03'/%3E%3C/svg%3E");
      pointer-events: none;
      z-index: 0;
      opacity: 0.4;
    }

    /* GLOW BLOBS */
    .blob {
      position: fixed;
      border-radius: 50%;
      filter: blur(120px);
      opacity: 0.12;
      pointer-events: none;
      z-index: 0;
    }
    .blob-1 { width: 500px; height: 500px; background: var(--accent2); top: -100px; right: -100px; }
    .blob-2 { width: 400px; height: 400px; background: var(--accent); bottom: 100px; left: -100px; }

    /* NAV */
    nav {
      position: fixed;
      top: 0; left: 0; right: 0;
      z-index: 100;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 1.2rem 5%;
      background: rgba(5,8,16,0.8);
      backdrop-filter: blur(20px);
      border-bottom: 1px solid var(--border);
    }

    .nav-logo {
      font-family: 'Space Mono', monospace;
      font-size: 1rem;
      color: var(--accent);
      letter-spacing: 0.05em;
    }

    .nav-links {
      display: flex;
      gap: 2rem;
      list-style: none;
    }

    .nav-links a {
      color: var(--muted);
      text-decoration: none;
      font-size: 0.85rem;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      transition: color 0.3s;
    }

    .nav-links a:hover { color: var(--accent); }

    .nav-cta {
      background: transparent;
      border: 1px solid var(--accent);
      color: var(--accent);
      padding: 0.5rem 1.2rem;
      font-family: 'Space Mono', monospace;
      font-size: 0.75rem;
      cursor: pointer;
      letter-spacing: 0.05em;
      transition: all 0.3s;
    }
    .nav-cta:hover { background: var(--accent); color: var(--bg); }

    /* HERO */
    .hero {
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      padding: 8rem 5% 4rem;
      position: relative;
      z-index: 1;
    }

    .hero-tag {
      font-family: 'Space Mono', monospace;
      font-size: 0.75rem;
      color: var(--accent);
      letter-spacing: 0.2em;
      text-transform: uppercase;
      margin-bottom: 1.5rem;
      display: flex;
      align-items: center;
      gap: 0.8rem;
      animation: fadeUp 0.8s ease both;
    }

    .hero-tag::before {
      content: '';
      width: 2rem;
      height: 1px;
      background: var(--accent);
    }

    .hero-title {
      font-size: clamp(3rem, 10vw, 7rem);
      font-weight: 800;
      line-height: 1.0;
      letter-spacing: -0.02em;
      margin-bottom: 1.5rem;
      animation: fadeUp 0.8s 0.1s ease both;
    }

    .hero-title .line2 {
      background: linear-gradient(90deg, var(--accent), var(--accent2));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }

    .hero-desc {
      font-size: 1.1rem;
      color: var(--muted);
      max-width: 520px;
      line-height: 1.7;
      margin-bottom: 3rem;
      animation: fadeUp 0.8s 0.2s ease both;
    }

    .hero-actions {
      display: flex;
      gap: 1rem;
      flex-wrap: wrap;
      animation: fadeUp 0.8s 0.3s ease both;
    }

    .btn-primary {
      background: linear-gradient(135deg, var(--accent), var(--accent2));
      color: var(--bg);
      border: none;
      padding: 0.9rem 2rem;
      font-family: 'Syne', sans-serif;
      font-weight: 600;
      font-size: 0.9rem;
      cursor: pointer;
      letter-spacing: 0.03em;
      transition: all 0.3s;
      text-decoration: none;
      display: inline-block;
    }
    .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 10px 40px rgba(0,245,212,0.3); }

    .btn-outline {
      background: transparent;
      color: var(--text);
      border: 1px solid var(--border);
      padding: 0.9rem 2rem;
      font-family: 'Syne', sans-serif;
      font-weight: 600;
      font-size: 0.9rem;
      cursor: pointer;
      letter-spacing: 0.03em;
      transition: all 0.3s;
      text-decoration: none;
      display: inline-block;
    }
    .btn-outline:hover { border-color: var(--accent); color: var(--accent); }

    /* STATS BAR */
    .stats-bar {
      position: relative;
      z-index: 1;
      display: flex;
      gap: 0;
      border-top: 1px solid var(--border);
      border-bottom: 1px solid var(--border);
      margin: 0 0 5rem;
      animation: fadeUp 0.8s 0.4s ease both;
    }

    .stat {
      flex: 1;
      padding: 1.5rem 5%;
      border-right: 1px solid var(--border);
    }
    .stat:last-child { border-right: none; }

    .stat-num {
      font-family: 'Space Mono', monospace;
      font-size: 1.8rem;
      color: var(--accent);
      font-weight: 700;
    }

    .stat-label {
      font-size: 0.75rem;
      color: var(--muted);
      letter-spacing: 0.1em;
      text-transform: uppercase;
      margin-top: 0.3rem;
    }

    /* SECTIONS */
    section {
      position: relative;
      z-index: 1;
      padding: 5rem 5%;
    }

    .section-tag {
      font-family: 'Space Mono', monospace;
      font-size: 0.7rem;
      color: var(--accent);
      letter-spacing: 0.2em;
      text-transform: uppercase;
      margin-bottom: 1rem;
      display: flex;
      align-items: center;
      gap: 0.8rem;
    }
    .section-tag::before { content: '//'; opacity: 0.5; }

    .section-title {
      font-size: clamp(2rem, 5vw, 3.5rem);
      font-weight: 800;
      letter-spacing: -0.02em;
      margin-bottom: 3rem;
    }

    /* SERVICES */
    .services-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 1px;
      background: var(--border);
      border: 1px solid var(--border);
    }

    .service-card {
      background: var(--card);
      padding: 2.5rem 2rem;
      transition: background 0.3s;
      cursor: default;
    }
    .service-card:hover { background: #111829; }

    .service-icon {
      font-size: 2rem;
      margin-bottom: 1.2rem;
    }

    .service-title {
      font-size: 1.2rem;
      font-weight: 700;
      margin-bottom: 0.8rem;
      letter-spacing: -0.01em;
    }

    .service-desc {
      font-size: 0.9rem;
      color: var(--muted);
      line-height: 1.6;
    }

    .service-price {
      margin-top: 1.5rem;
      font-family: 'Space Mono', monospace;
      font-size: 0.8rem;
      color: var(--accent);
    }

    /* PROJECTS */
    .projects-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
      gap: 1.5rem;
    }

    .project-card {
      background: var(--card);
      border: 1px solid var(--border);
      overflow: hidden;
      transition: transform 0.3s, border-color 0.3s;
    }
    .project-card:hover { transform: translateY(-4px); border-color: var(--accent); }

    .project-thumb {
      height: 180px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 4rem;
      position: relative;
      overflow: hidden;
    }

    .project-thumb-1 { background: linear-gradient(135deg, #0d1a2d, #1a2a4a); }
    .project-thumb-2 { background: linear-gradient(135deg, #1a0d2d, #2a1a4a); }
    .project-thumb-3 { background: linear-gradient(135deg, #0d2d1a, #1a4a2a); }

    .project-info { padding: 1.5rem; }

    .project-tags {
      display: flex;
      gap: 0.5rem;
      flex-wrap: wrap;
      margin-bottom: 0.8rem;
    }

    .tag {
      font-family: 'Space Mono', monospace;
      font-size: 0.65rem;
      padding: 0.2rem 0.6rem;
      background: rgba(0,245,212,0.08);
      color: var(--accent);
      border: 1px solid rgba(0,245,212,0.2);
      letter-spacing: 0.05em;
    }

    .tag-purple {
      background: rgba(123,97,255,0.08);
      color: var(--accent2);
      border-color: rgba(123,97,255,0.2);
    }

    .project-title {
      font-size: 1.1rem;
      font-weight: 700;
      margin-bottom: 0.5rem;
    }

    .project-desc {
      font-size: 0.85rem;
      color: var(--muted);
      line-height: 1.5;
    }

    /* PROCESS */
    .process-steps {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 0;
      position: relative;
    }

    .process-step {
      padding: 2rem;
      border: 1px solid var(--border);
      margin: -1px 0 0 -1px;
      position: relative;
      transition: background 0.3s;
    }
    .process-step:hover { background: var(--card); }

    .step-num {
      font-family: 'Space Mono', monospace;
      font-size: 3rem;
      font-weight: 700;
      color: rgba(0,245,212,0.1);
      margin-bottom: 1rem;
      line-height: 1;
    }

    .step-title {
      font-size: 1rem;
      font-weight: 700;
      margin-bottom: 0.5rem;
    }

    .step-desc {
      font-size: 0.85rem;
      color: var(--muted);
      line-height: 1.5;
    }

    /* TECH STACK */
    .tech-stack {
      display: flex;
      flex-wrap: wrap;
      gap: 0.8rem;
      margin-top: 2rem;
    }

    .tech-pill {
      font-family: 'Space Mono', monospace;
      font-size: 0.75rem;
      padding: 0.5rem 1rem;
      border: 1px solid var(--border);
      color: var(--muted);
      letter-spacing: 0.05em;
      transition: all 0.3s;
    }
    .tech-pill:hover { border-color: var(--accent); color: var(--accent); }

    /* CONTACT */
    .contact-section {
      background: var(--bg2);
      border-top: 1px solid var(--border);
      border-bottom: 1px solid var(--border);
    }

    .contact-inner {
      max-width: 600px;
    }

    .contact-form {
      display: flex;
      flex-direction: column;
      gap: 1rem;
      margin-top: 2rem;
    }

    .form-group {
      display: flex;
      flex-direction: column;
      gap: 0.4rem;
    }

    .form-label {
      font-family: 'Space Mono', monospace;
      font-size: 0.7rem;
      color: var(--muted);
      letter-spacing: 0.1em;
      text-transform: uppercase;
    }

    .form-input, .form-textarea {
      background: var(--card);
      border: 1px solid var(--border);
      color: var(--text);
      padding: 0.9rem 1rem;
      font-family: 'Syne', sans-serif;
      font-size: 0.9rem;
      outline: none;
      transition: border-color 0.3s;
    }
    .form-input:focus, .form-textarea:focus { border-color: var(--accent); }
    .form-textarea { min-height: 120px; resize: vertical; }

    /* FOOTER */
    footer {
      position: relative;
      z-index: 1;
      padding: 2rem 5%;
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 1rem;
      border-top: 1px solid var(--border);
    }

    .footer-copy {
      font-family: 'Space Mono', monospace;
      font-size: 0.75rem;
      color: var(--muted);
    }

    .footer-links {
      display: flex;
      gap: 1.5rem;
    }

    .footer-links a {
      font-size: 0.8rem;
      color: var(--muted);
      text-decoration: none;
      transition: color 0.3s;
    }
    .footer-links a:hover { color: var(--accent); }

    /* STATUS DOT */
    .status {
      display: flex;
      align-items: center;
      gap: 0.5rem;
      font-family: 'Space Mono', monospace;
      font-size: 0.7rem;
      color: var(--accent);
    }

    .dot {
      width: 8px; height: 8px;
      background: var(--accent);
      border-radius: 50%;
      animation: pulse 2s infinite;
    }

    @keyframes pulse {
      0%, 100% { opacity: 1; transform: scale(1); }
      50% { opacity: 0.5; transform: scale(0.8); }
    }

    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(24px); }
      to { opacity: 1; transform: translateY(0); }
    }

    /* MOBILE */
    @media (max-width: 768px) {
      nav { padding: 1rem 4%; }
      .nav-links { display: none; }
      .hero { padding: 7rem 4% 3rem; }
      .stats-bar { flex-direction: column; }
      .stat { border-right: none; border-bottom: 1px solid var(--border); }
      .stat:last-child { border-bottom: none; }
      section { padding: 3rem 4%; }
      footer { flex-direction: column; align-items: flex-start; }
    }
  </style>
</head>
<body>

  <div class="blob blob-1"></div>
  <div class="blob blob-2"></div>

  <!-- NAV -->
  <nav>
    <div class="nav-logo">yashraj.dev</div>
    <ul class="nav-links">
      <li><a href="#services">Services</a></li>
      <li><a href="#projects">Projects</a></li>
      <li><a href="#process">Process</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
    <button class="nav-cta" onclick="document.getElementById('contact').scrollIntoView({behavior:'smooth'})">Hire Me</button>
  </nav>

  <!-- HERO -->
  <section class="hero">
    <div class="hero-tag">Available for freelance work</div>
    <h1 class="hero-title">
      I Build<br/>
      <span class="line2">AI-Powered</span><br/>
      Experiences.
    </h1>
    <p class="hero-desc">
      Vibe coder & AI developer from Lucknow. I turn ideas into working products using the latest AI tools — fast, smart, and without the fluff.
    </p>
    <div class="hero-actions">
      <a href="#projects" class="btn-primary">See My Work</a>
      <a href="#contact" class="btn-outline">Let's Talk</a>
    </div>
  </section>

  <!-- STATS -->
  <div class="stats-bar">
    <div class="stat">
      <div class="stat-num">10+</div>
      <div class="stat-label">Projects Built</div>
    </div>
    <div class="stat">
      <div class="stat-num">48hr</div>
      <div class="stat-label">Avg Delivery</div>
    </div>
    <div class="stat">
      <div class="stat-num">100%</div>
      <div class="stat-label">Satisfaction</div>
    </div>
    <div class="stat">
      <div class="status">
        <div class="dot"></div>
        Open to Work
      </div>
      <div class="stat-label" style="margin-top:0.5rem">Based in Lucknow, IN</div>
    </div>
  </div>

  <!-- SERVICES -->
  <section id="services">
    <div class="section-tag">What I Do</div>
    <h2 class="section-title">Services</h2>
    <div class="services-grid">
      <div class="service-card">
        <div class="service-icon">🤖</div>
        <div class="service-title">AI Chatbots & Agents</div>
        <p class="service-desc">Custom AI chatbots and autonomous agents for your business — customer support, automation, or anything you can imagine.</p>
        <div class="service-price">Starting ₹2,999</div>
      </div>
      <div class="service-card">
        <div class="service-icon">🌐</div>
        <div class="service-title">Web Development</div>
        <p class="service-desc">Fast, modern websites and web apps. Landing pages, portfolios, dashboards — built and deployed quickly.</p>
        <div class="service-price">Starting ₹1,499</div>
      </div>
      <div class="service-card">
        <div class="service-icon">⚡</div>
        <div class="service-title">Prompt Engineering</div>
        <p class="service-desc">Get the most out of AI tools. Custom prompts, workflows, and AI integrations tailored to your specific needs.</p>
        <div class="service-price">Starting ₹999</div>
      </div>
      <div class="service-card">
        <div class="service-icon">🔧</div>
        <div class="service-title">AI Tool Integration</div>
        <p class="service-desc">Add AI superpowers to your existing product. API integrations, automation pipelines, and smart features.</p>
        <div class="service-price">Starting ₹3,999</div>
      </div>
    </div>
  </section>

  <!-- PROJECTS -->
  <section id="projects">
    <div class="section-tag">My Work</div>
    <h2 class="section-title">Projects</h2>
    <div class="projects-grid">
      <div class="project-card">
        <div class="project-thumb project-thumb-1">🤖</div>
        <div class="project-info">
          <div class="project-tags">
            <span class="tag">AI</span>
            <span class="tag tag-purple">Lovable.dev</span>
          </div>
          <div class="project-title">AI Support Chatbot</div>
          <p class="project-desc">An intelligent chatbot that handles customer queries 24/7 using advanced language models.</p>
        </div>
      </div>
      <div class="project-card">
        <div class="project-thumb project-thumb-2">🚀</div>
        <div class="project-info">
          <div class="project-tags">
            <span class="tag">Web App</span>
            <span class="tag tag-purple">React</span>
          </div>
          <div class="project-title">Portfolio Generator</div>
          <p class="project-desc">AI-powered tool that generates a complete developer portfolio from a simple form input.</p>
        </div>
      </div>
      <div class="project-card">
        <div class="project-thumb project-thumb-3">⚙️</div>
        <div class="project-info">
          <div class="project-tags">
            <span class="tag">Automation</span>
            <span class="tag tag-purple">AI Agent</span>
          </div>
          <div class="project-title">Content AI Agent</div>
          <p class="project-desc">Autonomous agent that researches, writes, and publishes content on a schedule.</p>
        </div>
      </div>
    </div>
  </section>

  <!-- PROCESS -->
  <section id="process">
    <div class="section-tag">How It Works</div>
    <h2 class="section-title">My Process</h2>
    <div class="process-steps">
      <div class="process-step">
        <div class="step-num">01</div>
        <div class="step-title">You Share the Idea</div>
        <p class="step-desc">Tell me what you want to build. No tech knowledge needed — just your vision.</p>
      </div>
      <div class="process-step">
        <div class="step-num">02</div>
        <div class="step-title">I Plan & Estimate</div>
        <p class="step-desc">I'll break it down, suggest the best approach, and give you a fair price.</p>
      </div>
      <div class="process-step">
        <div class="step-num">03</div>
        <div class="step-title">Fast Execution</div>
        <p class="step-desc">Using AI tools, I build faster than traditional developers without cutting corners.</p>
      </div>
      <div class="process-step">
        <div class="step-num">04</div>
        <div class="step-title">Deliver & Support</div>
        <p class="step-desc">You get a working product + free revisions. I stick around for questions.</p>
      </div>
    </div>

    <div style="margin-top: 4rem;">
      <div class="section-tag">Tech Stack</div>
      <div class="tech-stack">
        <span class="tech-pill">Claude AI</span>
        <span class="tech-pill">ChatGPT</span>
        <span class="tech-pill">Lovable.dev</span>
        <span class="tech-pill">React</span>
        <span class="tech-pill">HTML/CSS/JS</span>
        <span class="tech-pill">GitHub</span>
        <span class="tech-pill">Vercel</span>
        <span class="tech-pill">Prompt Engineering</span>
        <span class="tech-pill">AI Agents</span>
        <span class="tech-pill">REST APIs</span>
      </div>
    </div>
  </s
