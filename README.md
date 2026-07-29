<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Aeon Logics — Rust Ecosystem Engineering</title>
  <style>
    /* -----------------------------------------------------------------------------
       Aeon Logics Design Tokens (Hardcoded from SCSS)
       ----------------------------------------------------------------------------- */
    :root {
      --grey-900: #07080a;
      --grey-800: #0f1115;
      --grey-700: #1a1d24;
      --grey-400: #8792a6;
      --grey-100: #f4f6f8;
      
      --purple-glow: #bd5eff;   /* Electric purple */
      --purple-matrix: #9d4edd; /* Medium vibrant purple */
      --purple-dark: #5a189a;   /* Deep rich purple */

      /* Theme Assignment: Premium Dark Mode */
      --color-bg-base: var(--grey-900);
      --color-bg-surface: var(--grey-800);
      --color-border-subtle: var(--grey-700);
      
      --gradient-hero: linear-gradient(135deg, var(--grey-900) 0%, var(--purple-dark) 150%);
      --gradient-card: linear-gradient(180deg, rgba(15, 17, 21, 0.8) 0%, var(--grey-800) 100%);
      
      --color-accent-primary: var(--purple-glow);
      --color-accent-secondary: var(--purple-matrix);
      
      --text-high-contrast: var(--grey-100);
      --text-low-contrast: var(--grey-400);
      --text-on-primary: #ffffff;
      
      --font-family-system: "Geist", "Plus Jakarta Sans", system-ui, sans-serif;
      --font-family-data: "Commit Mono", "Intel One Mono", monospace;
    }

    /* -----------------------------------------------------------------------------
       Global Reset & Structural Layout
       ----------------------------------------------------------------------------- */
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      background-color: var(--color-bg-base);
      color: var(--text-low-contrast);
      font-family: var(--font-family-system);
      line-height: 1.6;
      padding-bottom: 80px;
    }

    /* -----------------------------------------------------------------------------
       Top Ambient Banner (Updated for responsive image handling)
       ----------------------------------------------------------------------------- */
    .top-banner {
      width: 100%;
      height: 180px;
      background: linear-gradient(135deg, var(--purple-dark) 0%, #240046 50%, var(--grey-900) 100%);
      position: relative;
      overflow: hidden;
      border-bottom: 1px solid var(--color-border-subtle);
    }

    /* Ensures the banner.png spans beautifully across all screen aspect ratios */
    .banner-img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      object-position: center;
      display: block;
    }

    /* Container matching Windows design width limits */
    .container {
      max-width: 1050px;
      margin: 0 auto;
      padding: 0 24px;
    }

    /* -----------------------------------------------------------------------------
       Company Profile Header Section
       ----------------------------------------------------------------------------- */
    .profile-header {
      position: relative;
      margin-top: -60px; /* Pull up to overlay onto banner beautifully */
      margin-bottom: 48px;
    }

    .brand-avatar {
      width: 110px;
      height: 110px;
      background: var(--gradient-card);
      border: 3px solid var(--color-accent-primary);
      border-radius: 24px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 2.5rem;
      font-weight: 800;
      color: var(--text-high-contrast);
      box-shadow: 0 12px 40px rgba(189, 94, 255, 0.25);
      font-family: var(--font-family-data);
    }

    .profile-info {
      margin-top: 20px;
      display: flex;
      flex-direction: column;
      gap: 8px;
    }

    .company-title-row {
      display: flex;
      align-items: center;
      gap: 16px;
      flex-wrap: wrap;
    }

    .company-name {
      font-size: 2.5rem;
      font-weight: 800;
      color: var(--text-high-contrast);
      letter-spacing: -0.03em;
    }

    .badge-rust {
      background: rgba(189, 94, 255, 0.1);
      border: 1px solid var(--color-accent-primary);
      color: var(--color-accent-primary);
      padding: 4px 12px;
      border-radius: 99px;
      font-size: 0.8rem;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.05em;
    }

    .tagline {
      font-size: 1.15rem;
      color: var(--text-high-contrast);
      max-width: 650px;
    }

    .meta-capabilities {
      display: flex;
      gap: 16px;
      font-size: var(--text-sm);
      font-family: var(--font-family-data);
      flex-wrap: wrap;
      margin-top: 4px;
    }

    .meta-item {
      display: flex;
      align-items: center;
      gap: 6px;
    }

    .meta-item::before {
      content: '⚡';
      color: var(--color-accent-secondary);
    }

    /* -----------------------------------------------------------------------------
       Web Apps / Projects Grid
       ----------------------------------------------------------------------------- */
    .section-title {
      font-size: var(--text-lg);
      color: var(--text-high-contrast);
      margin-bottom: 24px;
      letter-spacing: -0.01em;
      border-left: 4px solid var(--color-accent-primary);
      padding-left: 12px;
    }

    .projects-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(450px, 1fr));
      gap: 24px;
    }

    @media (max-width: 600px) {
      .projects-grid {
        grid-template-columns: 1fr;
      }
    }

    .card {
      background: var(--gradient-card);
      border: 1px solid var(--color-border-subtle);
      border-radius: 20px;
      padding: 32px;
      transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      position: relative;
      overflow: hidden;
    }

    .card::before {
      content: '';
      position: absolute;
      top: 0; left: 0; right: 0; bottom: 0;
      border-radius: 20px;
      padding: 1px;
      background: linear-gradient(to bottom, var(--color-border-subtle), transparent);
      -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
      -webkit-mask-composite: xor;
      mask-composite: exclude;
      pointer-events: none;
    }

    .card:hover {
      transform: translateY(-4px);
      border-color: rgba(189, 94, 255, 0.4);
      box-shadow: 0 20px 40px rgba(0,0,0,0.4), 0 0 30px rgba(189, 94, 255, 0.1);
    }

    .card-header h3 {
      font-size: var(--text-xl);
      color: var(--text-high-contrast);
      margin-bottom: 12px;
      display: flex;
      align-items: center;
      justify-content: space-between;
    }

    .card-desc {
      font-size: var(--text-sm);
      color: var(--text-low-contrast);
      margin-bottom: 24px;
      min-height: 48px;
    }

    .tech-stack-row {
      display: flex;
      gap: 8px;
      margin-bottom: 24px;
      flex-wrap: wrap;
    }

    .tech-pill {
      font-family: var(--font-family-data);
      font-size: var(--text-xs);
      background: #161920;
      padding: 4px 10px;
      border-radius: 6px;
      border: 1px solid var(--color-border-subtle);
    }

    .card-footer {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .card-link {
      color: var(--color-accent-primary);
      text-decoration: none;
      font-size: var(--text-sm);
      font-weight: 600;
      display: inline-flex;
      align-items: center;
      gap: 6px;
      transition: color 0.2s;
    }

    .card-link:hover {
      color: var(--text-high-contrast);
    }

    .live-dot {
      width: 8px;
      height: 8px;
      background-color: #00e676;
      border-radius: 50%;
      box-shadow: 0 0 10px #00e676;
    }
  </style>
</head>
<body>

  <!-- Top Decorative Banner Overlay with responsive image wrapper -->
  <div class="top-banner">
    <img src="banner.png" alt="Aeon Logics Banner" class="banner-img" />
  </div>

  <div class="container">
    
    <!-- Profile Info Header Container -->
    <header class="profile-header">
      <div class="brand-avatar">æ</div>
      <div class="profile-info">
        <div class="company-title-row">
          <h1 class="company-name">Aeon Logics</h1>
          <span class="badge-rust">Rust Ecosystem</span>
        </div>
        <p class="tagline">Engineers of high-performance full-stack applications, custom desktop native experiences, microservices, and specialized databases.</p>
        <div class="meta-capabilities">
          <span class="meta-item">Frontend & Backend</span>
          <span class="meta-item">Desktop Systems</span>
          <span class="meta-item">Distributed Servers</span>
        </div>
      </div>
    </header>

    <!-- Main Dynamic Application Projects -->
    <main>
      <h2 class="section-title">Production Web Applications</h2>
      <div class="projects-grid">
        
        <!-- Application Card 1: GlassDB -->
        <article class="card">
          <div class="card-body">
            <div class="card-header">
              <h3>GlassDB <span class="live-dot" title="Active Deployment"></span></h3>
            </div>
            <p class="card-desc">An ultra-efficient, highly scalable database system natively designed inside the Rust storage layer environment to deliver robust, lightning-fast transaction executions.</p>
            <div class="tech-stack-row">
              <span class="tech-pill">Rust</span>
              <span class="tech-pill">ACID KV Store</span>
              <span class="tech-pill">Distributed Servers</span>
              <span class="tech-pill">Railway</span>
            </div>
          </div>
          <div class="card-footer">
            <a href="https://railway.app" target="_blank" class="card-link">Launch Live App ↗</a>
          </div>
