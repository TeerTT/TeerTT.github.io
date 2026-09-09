# TeerTT.github.io
<html lang="th">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Thanesuan Noikong (Teer) | 3D Portfolio & Voxel Studio</title>

  <!-- Google Fonts: Special Elite & Sarabun -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Sarabun:wght@300;400;600&family=Special+Elite&family=VT323&display=swap" rel="stylesheet">

  <style>
    :root {
      --cork-base: #865935;
      --cork-dark: #4d2f17;
      --paper-cream: #f4ebd0;
      --tape-color: rgba(235, 218, 166, 0.65);
      --string-red: #c92a2a;
      --pin-gold: #f59f00;
      --panel-bg: rgba(18, 22, 28, 0.88);
      --border-dark: #2f3846;
      --font-dossier: 'Special Elite', monospace;
      --font-thai: 'Sarabun', sans-serif;
      --font-crt: 'VT323', monospace;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      user-select: none;
    }

    body {
      background-color: #1a110b;
      color: #e2e8f0;
      font-family: var(--font-thai);
      overflow: hidden;
      width: 100vw;
      height: 100vh;
      position: relative;
    }

    /* 1. Detective Corkboard Background */
    #corkboard-canvas {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      z-index: 0;
    }

    /* Flashlight Overlay */
    #flashlight-overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      pointer-events: none;
      z-index: 2;
      background: radial-gradient(
        circle 380px at var(--mouse-x, 50%) var(--mouse-y, 50%),
        rgba(255, 235, 180, 0.08) 0%,
        rgba(10, 7, 4, 0.6) 45%,
        rgba(5, 3, 2, 0.92) 85%
      );
      mix-blend-mode: multiply;
    }

    /* 2. 3D WebGL Canvas for Voxel Painter */
    #webgl-canvas {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      z-index: 1;
    }

    /* 3. Center Detective Headline */
    .center-title-container {
      position: fixed;
      top: 36px;
      left: 50%;
      transform: translateX(-50%);
      z-index: 4;
      text-align: center;
      pointer-events: none;
      background: rgba(18, 14, 10, 0.75);
      border: 2px dashed rgba(229, 169, 60, 0.6);
      padding: 14px 28px;
      border-radius: 4px;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.7);
      backdrop-filter: blur(4px);
    }

    .main-name {
      font-family: var(--font-dossier);
      font-size: clamp(1.8rem, 3.8vw, 2.8rem);
      font-weight: 700;
      letter-spacing: 2px;
      color: #f8fafc;
      text-transform: uppercase;
      text-shadow: 0 2px 8px rgba(0,0,0,0.8);
    }

    .sub-dossier {
      font-size: 0.95rem;
      color: #eab308;
      font-family: var(--font-thai);
      font-weight: 400;
      margin-top: 4px;
      letter-spacing: 0.5px;
    }

    /* 4. Left Profile Dossier Card */
    .profile-card {
      position: fixed;
      top: 140px;
      left: 24px;
      z-index: 5;
      width: 320px;
      background: var(--panel-bg);
      border: 1px solid var(--border-dark);
      border-left: 4px solid #c92a2a;
      backdrop-filter: blur(8px);
      padding: 20px;
      border-radius: 6px;
      box-shadow: 0 16px 36px rgba(0, 0, 0, 0.75);
    }

    .card-stamp {
      position: absolute;
      top: 14px;
      right: 14px;
      color: #c92a2a;
      border: 2px solid #c92a2a;
      padding: 2px 6px;
      font-family: var(--font-dossier);
      font-size: 0.75rem;
      transform: rotate(6deg);
      letter-spacing: 1px;
    }

    .profile-title {
      font-family: var(--font-dossier);
      color: #f59f00;
      font-size: 0.9rem;
      margin-bottom: 8px;
      letter-spacing: 1px;
    }

    .profile-detail {
      font-size: 0.88rem;
      line-height: 1.6;
      color: #cbd5e1;
    }

    .profile-badge-row {
      display: flex;
      flex-wrap: wrap;
      gap: 6px;
      margin-top: 10px;
    }

    .badge-pill {
      background: rgba(245, 159, 0, 0.15);
      border: 1px solid rgba(245, 159, 0, 0.4);
      color: #fde047;
      font-size: 0.75rem;
      padding: 3px 8px;
      border-radius: 3px;
    }

    .instructions-box {
      margin-top: 14px;
      background: rgba(0, 0, 0, 0.35);
      border: 1px dashed #475569;
      padding: 10px;
      border-radius: 4px;
      font-size: 0.8rem;
      color: #94a3b8;
    }

    .instructions-box strong {
      color: #e2e8f0;
    }

    /* 5. Right Control Panel (Lighting & Rotation) */
    .control-panel {
      position: fixed;
      top: 140px;
      right: 24px;
      z-index: 5;
      width: 290px;
      background: var(--panel-bg);
      border: 1px solid var(--border-dark);
      border-left: 4px solid #f59f00;
      backdrop-filter: blur(8px);
      padding: 18px 20px;
      border-radius: 6px;
      box-shadow: 0 16px 36px rgba(0, 0, 0, 0.75);
      font-family: var(--font-dossier);
    }

    .panel-header {
      color: #f59f00;
      font-size: 0.95rem;
      margin-bottom: 12px;
      letter-spacing: 1px;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .ctrl-item {
      margin-bottom: 10px;
      display: flex;
      flex-direction: column;
      gap: 4px;
    }

    .ctrl-item label {
      font-size: 0.78rem;
      color: #94a3b8;
      display: flex;
      justify-content: space-between;
    }

    .ctrl-item input[type="range"] {
      -webkit-appearance: none;
      width: 100%;
      height: 4px;
      background: #334155;
      border-radius: 2px;
      outline: none;
    }

    .ctrl-item input[type="range"]::-webkit-slider-thumb {
      -webkit-appearance: none;
      width: 14px;
      height: 14px;
      border-radius: 50%;
      background: #f59f00;
      cursor: pointer;
      box-shadow: 0 0 6px #f59f00;
    }

    .color-picker-row {
      display: flex;
      gap: 6px;
      margin-top: 10px;
      align-items: center;
    }

    .color-swatch {
      width: 20px;
      height: 20px;
      border-radius: 3px;
      cursor: pointer;
      border: 2px solid transparent;
      transition: transform 0.15s;
    }

    .color-swatch.active {
      border-color: #fff;
      transform: scale(1.15);
    }

    .btn-row {
      display: flex;
      gap: 8px;
      margin-top: 12px;
      padding-top: 10px;
      border-top: 1px dashed var(--border-dark);
    }

    .btn-action {
      flex: 1;
      background: rgba(245, 159, 0, 0.12);
      border: 1px solid #f59f00;
      color: #f59f00;
      padding: 6px;
      font-size: 0.72rem;
      font-family: var(--font-dossier);
      cursor: pointer;
      border-radius: 3px;
      text-align: center;
      transition: all 0.2s;
    }

    .btn-action:hover, .btn-action.active {
      background: #f59f00;
      color: #000;
    }

    /* 6. Bottom Right Retro CRT TV */
    .tv-container {
      position: fixed;
      bottom: 24px;
      right: 24px;
      z-index: 5;
      width: 320px;
      background: #251e18;
      border: 4px solid #140f0c;
      border-radius: 12px;
      box-shadow: 0 20px 45px rgba(0, 0, 0, 0.9);
      padding: 12px 14px;
    }

    .tv-casing {
      display: flex;
      gap: 12px;
    }

    .tv-screen-wrapper {
      flex: 1;
      height: 180px;
      background: #090e0c;
      border-radius: 18px / 12px;
      border: 3px solid #101512;
      position: relative;
      overflow: hidden;
      box-shadow: inset 0 0 18px rgba(0, 0, 0, 0.95);
    }

    /* CRT scanlines effect */
    .tv-screen-wrapper::after {
      content: "";
      position: absolute;
      top: 0; left: 0; width: 100%; height: 100%;
      background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.35) 50%),
                  linear-gradient(90deg, rgba(255, 0, 0, 0.04), rgba(0, 255, 0, 0.02), rgba(0, 0, 255, 0.04));
      background-size: 100% 3px, 4px 100%;
      pointer-events: none;
      z-index: 3;
    }

    .tv-content-frame {
      width: 100%;
      height: 100%;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      padding: 10px;
      color: #4ade80;
      font-family: var(--font-crt);
      text-shadow: 0 0 5px rgba(74, 222, 128, 0.6);
      position: relative;
      z-index: 2;
    }

    .tv-badge-header {
      font-size: 1rem;
      display: flex;
      justify-content: space-between;
      letter-spacing: 1px;
    }

    .tv-project-name {
      font-size: 1.35rem;
      font-weight: 700;
      color: #86efac;
      margin-top: 4px;
      letter-spacing: 1px;
    }

    .tv-desc {
      font-size: 0.95rem;
      line-height: 1.25;
      color: #bbf7d0;
      margin-top: 4px;
      font-family: var(--font-thai);
    }

    .tv-meta {
      font-size: 0.85rem;
      color: #22c55e;
      display: flex;
      justify-content: space-between;
    }

    .tv-knobs {
      width: 45px;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: space-around;
    }

    .tv-dial {
      width: 32px;
      height: 32px;
      background: #181310;
      border: 2px solid #4a382c;
      border-radius: 50%;
      cursor: pointer;
      position: relative;
      transition: transform 0.2s;
    }

    .tv-dial::before {
      content: "";
      position: absolute;
      top: 4px;
      left: 50%;
      transform: translateX(-50%);
      width: 3px;
      height: 8px;
      background: #f59f00;
      border-radius: 2px;
    }

    .tv-dial:active {
      transform: rotate(45deg);
    }

    .tv-label {
      font-size: 0.6rem;
      font-family: var(--font-dossier);
      color: #a88871;
      text-align: center;
    }
  </style>

  <!-- Polyfill & Three.js Import map -->
  <script type="importmap">
    {
      "imports": {
        "three": "https://unpkg.com/three@0.160.0/build/three.module.js"
      }
    }
  </script>
</head>
<body>

  <!-- Corkboard 2D Canvas Background -->
  <canvas id="corkboard-canvas"></canvas>

  <!-- Flashlight Vignette Overlay -->
  <div id="flashlight-overlay"></div>

  <!-- Three.js Interactive 3D Voxel Studio Canvas -->
  <canvas id="webgl-canvas"></canvas>

  <!-- Center Headline Title -->
  <div class="center-title-container">
    <div class="main-name">Thanesuan Noikong</div>
    <div class="sub-dossier">Teer • นักศึกษาชั้นปีที่ 4 คณะสถาปัตย์เทคโนโลยี สาขาเกมและอนิเมชั่น</div>
  </div>

  <!-- Left: Dossier Bio & Instructions Card -->
  <div class="profile-card">
    <div class="card-stamp">CONFIDENTIAL</div>
    <div class="profile-title">INVESTIGATION FILE // SUBJECT BIO</div>
    <div class="profile-detail">
      มีความรู้พื้นฐานที่จำเป็นในการพัฒนาเกม 3D และทักษะด้าน Environment, Rigging และ Interactive Architecture
    </div>
    <div class="profile-badge-row">
      <span class="badge-pill">Unity</span>
      <span class="badge-pill">Blender</span>
      <span class="badge-pill">Maya</span>
      <span class="badge-pill">Affinity</span>
      <span class="badge-pill">C# Scripting</span>
    </div>
    <div class="instructions-box">
      <strong>🎯 3D Voxel Controls:</strong><br>
      • <strong>คลิกซ้าย:</strong> วางบล็อก 3D บนกริด<br>
      • <strong>Shift + คลิกซ้าย:</strong> ลบบล็อกที่ชี้<br>
      • <strong>คลิกขวา + ลาก:</strong> หมุนมุมมองกล้อง (Orbit)<br>
      • <strong>Scroll เมาส์:</strong> ซูมเข้า-ออก
    </div>
  </div>

  <!-- Right: 3D Lighting & Transform Control Panel -->
  <div class="control-panel">
    <div class="panel-header">⚙️ EVIDENCE CONTROLS</div>

    <div class="ctrl-item">
      <label for="sliderLight">ความสว่างไฟหลัก: <span id="lightVal">1.8</span></label>
      <input type="range" id="sliderLight" min="0.2" max="4.0" step="0.1" value="1.8" />
    </div>

    <div class="ctrl-item">
      <label for="sliderAmbient">แสงแวดล้อม (Ambient): <span id="ambientVal">0.6</span></label>
      <input type="range" id="sliderAmbient" min="0.0" max="2.0" step="0.05" value="0.6" />
    </div>

    <div class="ctrl-item">
      <label for="sliderRotY">หมุนวัตถุแกน Y: <span id="rotYVal">0°</span></label>
      <input type="range" id="sliderRotY" min="-180" max="180" step="1" value="0" />
    </div>

    <div class="ctrl-item">
      <label for="sliderRotX">หมุนวัตถุแกน X: <span id="rotXVal">0°</span></label>
      <input type="range" id="sliderRotX" min="-90" max="90" step="1" value="0" />
    </div>

    <div class="ctrl-item">
      <label>เลือกสี Voxel Paint:</label>
      <div class="color-picker-row">
        <div class="color-swatch active" style="background: #e5a93c;" data-color="0xe5a93c"></div>
        <div class="color-swatch" style="background: #c92a2a;" data-color="0xc92a2a"></div>
        <div class="color-swatch" style="background: #2b8a3e;" data-color="0x2b8a3e"></div>
        <div class="color-swatch" style="background: #1971c2;" data-color="0x1971c2"></div>
        <div class="color-swatch" style="background: #862e9c;" data-color="0x862e9c"></div>
        <div class="color-swatch" style="background: #e2e8f0;" data-color="0xe2e8f0"></div>
      </div>
    </div>

    <div class="btn-row">
      <button id="btnAutoSpin" class="btn-action">Auto-Spin: OFF</button>
      <button id="btnClear" class="btn-action">Clear All</button>
    </div>
  </div>

  <!-- Bottom Right: Retro CRT TV Exhibit -->
  <div class="tv-container">
    <div class="tv-casing">
      <div class="tv-screen-wrapper">
        <div class="tv-content-frame">
          <div>
            <div class="tv-badge-header">
              <span>CH-0<span id="tvChannelNum">1</span></span>
              <span>● REC [2026]</span>
            </div>
            <div class="tv-project-name" id="tvProjectTitle">CHEMICAL CRASHOUT</div>
          </div>
          <div class="tv-desc" id="tvProjectDesc">
            Unity Game Project: เกมจำลองห้องแล็บเคมี ระบบแต่งตัว PPE และจัดเก็บสารเคมี
          </div>
          <div class="tv-meta">
            <span id="tvProjectTool">ENGINE: Unity C#</span>
            <span>PORTFOLIO EXHIBIT</span>
          </div>
        </div>
      </div>

      <div class="tv-knobs">
        <div class="tv-dial" id="tvDialNext" title="Click to Change Channel"></div>
        <div class="tv-label">CHANNEL</div>
        <div class="tv-dial" id="tvDialPower" title="Power / Static"></div>
        <div class="tv-label">POWER</div>
      </div>
    </div>
  </div>

  <!-- Background Detective Board Script (2D Canvas) -->
  <script>
    const corkCanvas = document.getElementById('corkboard-canvas');
    const corkCtx = corkCanvas.getContext('2d');
    const overlay = document.getElementById('flashlight-overlay');

    let cw = (corkCanvas.width = window.innerWidth);
    let ch = (corkCanvas.height = window.innerHeight);

    window.addEventListener('resize', () => {
      cw = corkCanvas.width = window.innerWidth;
      ch = corkCanvas.height = window.innerHeight;
      drawDetectiveBoard();
    });

    // Track mouse for flashlight
    window.addEventListener('mousemove', (e) => {
      overlay.style.setProperty('--mouse-x', `${e.clientX}px`);
      overlay.style.setProperty('--mouse-y', `${e.clientY}px`);
    });

    // Generate Evidence Items on Board
    const pins = [
      { x: 0.18 * cw, y: 0.22 * ch, color: '#c92a2a', note: 'MAP A' },
      { x: 0.28 * cw, y: 0.16 * ch, color: '#f59f00', note: 'SUSPECT 01' },
      { x: 0.48 * cw, y: 0.20 * ch, color: '#c92a2a', note: 'EVIDENCE FILE' },
      { x: 0.72 * cw, y: 0.15 * ch, color: '#1971c2', note: 'MECH BLUEPRINT' },
      { x: 0.85 * cw, y: 0.28 * ch, color: '#c92a2a', note: 'CLASSIFIED' },
      { x: 0.15 * cw, y: 0.65 * ch, color: '#f59f00', note: 'LEVEL DESIGN' },
      { x: 0.42 * cw, y: 0.72 * ch, color: '#c92a2a', note: 'CRIME SCENE' },
      { x: 0.78 * cw, y: 0.68 * ch, color: '#f59f00', note: 'TARGET' }
    ];

    function drawDetectiveBoard() {
      // 1. Cork Texture Base
      const gradient = corkCtx.createRadialGradient(cw/2, ch/2, 100, cw/2, ch/2, Math.max(cw, ch));
      gradient.addColorStop(0, '#9c663b');
      gradient.addColorStop(0.7, '#6b4220');
      gradient.addColorStop(1, '#3b220e');
      corkCtx.fillStyle = gradient;
      corkCtx.fillRect(0, 0, cw, ch);

      // Add cork noise
      for (let i = 0; i < 2400; i++) {
        corkCtx.fillStyle = Math.random() > 0.5 ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.06)';
        corkCtx.fillRect(Math.random() * cw, Math.random() * ch, 2, 2);
      }

      // 2. Paper documents pinned to corkboard
      const papers = [
        { x: cw * 0.08, y: ch * 0.10, w: 220, h: 180, rot: -0.06, title: 'TOPOLOGY REPORT', lines: 6 },
        { x: cw * 0.68, y: ch * 0.08, w: 260, h: 200, rot: 0.04, title: 'CLASSIFIED // RIGGING', lines: 7 },
        { x: cw * 0.05, y: ch * 0.55, w: 200, h: 160, rot: 0.05, title: 'UNITY LAB AUDIT', lines: 5 },
        { x: cw * 0.38, y: ch * 0.70, w: 230, h: 170, rot: -0.03, title: 'ENVIRONMENT STUDY', lines: 5 }
      ];

      papers.forEach(p => {
        corkCtx.save();
        corkCtx.translate(p.x, p.y);
        corkCtx.rotate(p.rot);

        // Drop Shadow
        corkCtx.shadowColor = 'rgba(0,0,0,0.6)';
        corkCtx.shadowBlur = 15;
        corkCtx.shadowOffsetX = 6;
        corkCtx.shadowOffsetY = 8;

        // Paper
        corkCtx.fillStyle = '#f1e7d0';
        corkCtx.fillRect(0, 0, p.w, p.h);

        // Border
        corkCtx.strokeStyle = '#c8baa0';
        corkCtx.lineWidth = 1;
        corkCtx.strokeRect(0, 0, p.w, p.h);

        // Header
        corkCtx.shadowColor = 'transparent';
        corkCtx.fillStyle = '#473c33';
        corkCtx.font = '10px "Special Elite", monospace';
        corkCtx.fillText(p.title, 14, 22);

        // Content placeholder lines
        corkCtx.fillStyle = 'rgba(80, 70, 60, 0.4)';
        for (let l = 0; l < p.lines; l++) {
          corkCtx.fillRect(14, 38 + l * 18, p.w - 28, 4);
        }

        // Tape effect on corners
        corkCtx.fillStyle = 'rgba(240, 225, 175, 0.7)';
        corkCtx.fillRect(p.w / 2 - 25, -6, 50, 14);

        corkCtx.restore();
      });

      // 3. Connect Pins with Red Investigative String (ด้ายแดง)
      corkCtx.beginPath();
      corkCtx.strokeStyle = 'rgba(201, 42, 42, 0.85)';
      corkCtx.lineWidth = 2.5;
      corkCtx.shadowColor = 'rgba(0,0,0,0.7)';
      corkCtx.shadowBlur = 4;
      corkCtx.shadowOffsetY = 4;

      for (let i = 0; i < pins.length - 1; i++) {
        corkCtx.moveTo(pins[i].x, pins[i].y);
        corkCtx.lineTo(pins[i+1].x, pins[i+1].y);
      }
      corkCtx.stroke();

      // Additional cross-reference lines
      corkCtx.beginPath();
      corkCtx.moveTo(pins[0].x, pins[0].y);
      corkCtx.lineTo(pins[2].x, pins[2].y);
      corkCtx.moveTo(pins[3].x, pins[3].y);
      corkCtx.lineTo(pins[6].x, pins[6].y);
      corkCtx.moveTo(pins[1].x, pins[1].y);
      corkCtx.lineTo(pins[5].x, pins[5].y);
      corkCtx.stroke();

      // 4. Draw Pins
      corkCtx.shadowColor = 'rgba(0,0,0,0.8)';
      corkCtx.shadowBlur = 8;
      corkCtx.shadowOffsetX = 3;
      corkCtx.shadowOffsetY = 5;

      pins.forEach(pin => {
        corkCtx.beginPath();
        corkCtx.arc(pin.x, pin.y, 6.5, 0, Math.PI * 2);
        corkCtx.fillStyle = pin.color;
        corkCtx.fill();
        corkCtx.strokeStyle = '#fff';
        corkCtx.lineWidth = 1.5;
        corkCtx.stroke();
      });
    }

    drawDetectiveBoard();
  </script>

  <!-- Interactive 3D Voxel Studio Script (Three.js) -->
  <script type="module">
    import * as THREE from 'three';

    // 1. Scene, Camera, Renderer
    const canvas = document.querySelector('#webgl-canvas');
    const scene = new THREE.Scene();

    const camera = new THREE.PerspectiveCamera(45, window.innerWidth / window.innerHeight, 0.1, 1000);
    camera.position.set(16, 20, 24);
    camera.lookAt(0, 0, 0);

    const renderer = new THREE.WebGLRenderer({ canvas, antialias: true, alpha: true });
    renderer.setSize(window.innerWidth, window.innerHeight);
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
    renderer.shadowMap.enabled = true;
    renderer.shadowMap.type = THREE.PCFSoftShadowMap;

    // 2. Voxel Objects & Workspace
    const voxelGroup = new THREE.Group();
    scene.add(voxelGroup);

    const boxGeo = new THREE.BoxGeometry(1, 1, 1);
    const boxMaterials = new Map(); // Cache materials by color

    function getVoxelMaterial(hexColor) {
      if (!boxMaterials.has(hexColor)) {
        boxMaterials.set(hexColor, new THREE.MeshStandardMaterial({
          color: hexColor,
          roughness: 0.35,
          metalness: 0.15,
        }));
      }
      return boxMaterials.get(hexColor);
    }

    let currentColor = 0xe5a93c;

    // Roll-over Helper Cube (ไกด์บอกตำแหน่งเมาส์)
    const rollOverGeo = new THREE.BoxGeometry(1.02, 1.02, 1.02);
    const rollOverMat = new THREE.MeshBasicMaterial({
      color: 0xef4444,
      opacity: 0.45,
      transparent: true,
      wireframe: true
    });
    const rollOverMesh = new THREE.Mesh(rollOverGeo, rollOverMat);
    scene.add(rollOverMesh);

    // Interactive Ground Grid Plane
    const gridSize = 16;
    const gridHelper = new THREE.GridHelper(gridSize, gridSize, 0xe5a93c, 0x475569);
    gridHelper.position.y = -0.01;
    voxelGroup.add(gridHelper);

    const planeGeo = new THREE.PlaneGeometry(gridSize, gridSize);
    planeGeo.rotateX(-Math.PI / 2);
    const planeMat = new THREE.MeshBasicMaterial({ visible: false });
    const groundPlane = new THREE.Mesh(planeGeo, planeMat);
    voxelGroup.add(groundPlane);

    // Collision target list for raycasting
    const objects = [groundPlane];

    // Seed Initial Voxel Diorama (ตั้งเสาตัวอย่างไว้ให้เล่น)
    function addInitialVoxel(x, y, z, color) {
      const voxel = new THREE.Mesh(boxGeo, getVoxelMaterial(color));
      voxel.position.set(x + 0.5, y + 0.5, z + 0.5);
      voxel.castShadow = true;
      voxel.receiveShadow = true;
      voxelGroup.add(voxel);
      objects.push(voxel);
    }

    // สร้างแท่นโมเดลตัวอย่างใจกลางกริด
    for (let x = -2; x <= 2; x++) {
      for (let z = -2; z <= 2; z++) {
        addInitialVoxel(x, 0, z, 0x2f3846);
      }
    }
    addInitialVoxel(0, 1, 0, 0xe5a93c);
    addInitialVoxel(0, 2, 0, 0xe5a93c);
    addInitialVoxel(1, 1, 0, 0xc92a2a);
    addInitialVoxel(-1, 1, 0, 0x1971c2);

    // 3. Lighting
    const ambientLight = new THREE.AmbientLight(0xffffff, 0.6);
    scene.add(ambientLight);

    const dirLight = new THREE.DirectionalLight(0xfff4d6, 1.8);
    dirLight.position.set(15, 25, 12);
    dirLight.castShadow = true;
    dirLight.shadow.mapSize.width = 1024;
    dirLight.shadow.mapSize.height = 1024;
    dirLight.shadow.camera.near = 0.5;
    dirLight.shadow.camera.far = 50;
    dirLight.shadow.camera.left = -15;
    dirLight.shadow.camera.right = 15;
    dirLight.shadow.camera.top = 15;
    dirLight.shadow.camera.bottom = -15;
    scene.add(dirLight);

    const blueRimLight = new THREE.PointLight(0x38bdf8, 20, 40);
    blueRimLight.position.set(-15, 10, -15);
    scene.add(blueRimLight);

    // 4. Raycasting & Interaction
    const raycaster = new THREE.Raycaster();
    const mouse = new THREE.Vector2();
    let isShiftDown = false;
    let isOrbiting = false;
    let prevMousePos = { x: 0, y: 0 };
    let cameraSpherical = { radius: 32, theta: Math.PI / 4, phi: Math.PI / 3.2 };

    function updateCameraFromSpherical() {
      camera.position.x = cameraSpherical.radius * Math.sin(cameraSpherical.phi) * Math.sin(cameraSpherical.theta);
      camera.position.y = cameraSpherical.radius * Math.cos(cameraSpherical.phi);
      camera.position.z = cameraSpherical.radius * Math.sin(cameraSpherical.phi) * Math.cos(cameraSpherical.theta);
      camera.lookAt(0, 1, 0);
    }
    updateCameraFromSpherical();

    window.addEventListener('pointermove', (event) => {
      mouse.x = (event.clientX / window.innerWidth) * 2 - 1;
      mouse.y = -(event.clientY / window.innerHeight) * 2 + 1;

      // Handle Right-Click Camera Orbit Drag
      if (isOrbiting) {
        const deltaX = event.clientX - prevMousePos.x;
        const deltaY = event.clientY - prevMousePos.y;

        cameraSpherical.theta -= deltaX * 0.008;
        cameraSpherical.phi = Math.max(0.1, Math.min(Math.PI / 2 - 0.05, cameraSpherical.phi - deltaY * 0.008));
        updateCameraFromSpherical();

        prevMousePos = { x: event.clientX, y: event.clientY };
        return;
      }

      // Update Roll-Over Helper Cube
      raycaster.setFromCamera(mouse, camera);
      const intersects = raycaster.intersectObjects(objects, false);

      if (intersects.length > 0) {
        const intersect = intersects[0];
        if (isShiftDown) {
          if (intersect.object !== groundPlane) {
            rollOverMesh.visible = true;
            rollOverMesh.position.copy(intersect.object.position);
          } else {
            rollOverMesh.visible = false;
          }
        } else {
          rollOverMesh.visible = true;
          const position = new THREE.Vector3();
          position.addVectors(intersect.point, intersect.face.normal);
          position.floor().addScalar(0.5);
          rollOverMesh.position.copy(position);
        }
      } else {
        rollOverMesh.visible = false;
      }
    });

    window.addEventListener('pointerdown', (event) => {
      // ตรวจสอบว่าไม่คลิกโดน UI Card / Controls
      if (event.target.closest('.profile-card, .control-panel, .tv-container, .center-title-container')) {
        return;
      }

      if (event.button === 2) {
        // Right Click: Camera Orbit
        isOrbiting = true;
        prevMousePos = { x: event.clientX, y: event.clientY };
        return;
      }

      if (event.button === 0) {
        // Left Click: Place or Delete Voxel
        raycaster.setFromCamera(mouse, camera);
        const intersects = raycaster.intersectObjects(objects, false);

        if (intersects.length > 0) {
          const intersect = intersects[0];

          // Delete Voxel
          if (isShiftDown) {
            if (intersect.object !== groundPlane) {
              voxelGroup.remove(intersect.object);
              objects.splice(objects.indexOf(intersect.object), 1);
              intersect.object.geometry.dispose();
              rollOverMesh.visible = false;
            }
          } 
          // Place Voxel
          else {
            const voxel = new THREE.Mesh(boxGeo, getVoxelMaterial(currentColor));
            voxel.castShadow = true;
            voxel.receiveShadow = true;

            const position = new THREE.Vector3();
            position.addVectors(intersect.point, intersect.face.normal);
            position.floor().addScalar(0.5);

            // เช็กขอบเขต Grid
            if (Math.abs(position.x) <= gridSize / 2 && Math.abs(position.z) <= gridSize / 2) {
              voxel.position.copy(position);
              voxelGroup.add(voxel);
              objects.push(voxel);
            }
          }
        }
      }
    });

    window.addEventListener('pointerup', (event) => {
      if (event.button === 2) isOrbiting = false;
    });

    window.addEventListener('contextmenu', (e) => e.preventDefault());

    // Zooming with wheel
    window.addEventListener('wheel', (e) => {
      cameraSpherical.radius = Math.max(8, Math.min(50, cameraSpherical.radius + e.deltaY * 0.03));
      updateCameraFromSpherical();
    });

    window.addEventListener('keydown', (e) => {
      if (e.key === 'Shift') isShiftDown = true;
    });
    window.addEventListener('keyup', (e) => {
      if (e.key === 'Shift') isShiftDown = false;
    });

    // 5. Control Panel UI Listeners
    const sliderLight = document.getElementById('sliderLight');
    const lightVal = document.getElementById('lightVal');
    const sliderAmbient = document.getElementById('sliderAmbient');
    const ambientVal = document.getElementById('ambientVal');
    const sliderRotY = document.getElementById('sliderRotY');
    const rotYVal = document.getElementById('rotYVal');
    const sliderRotX = document.getElementById('sliderRotX');
    const rotXVal = document.getElementById('rotXVal');
    const btnAutoSpin = document.getElementById('btnAutoSpin');
    const btnClear = document.getElementById('btnClear');

    sliderLight.addEventListener('input', (e) => {
      const val = parseFloat(e.target.value);
      dirLight.intensity = val;
      lightVal.textContent = val.toFixed(1);
    });

    sliderAmbient.addEventListener('input', (e) => {
      const val = parseFloat(e.target.value);
      ambientLight.intensity = val;
      ambientVal.textContent = val.toFixed(2);
    });

    sliderRotY.addEventListener('input', (e) => {
      const deg = parseInt(e.target.value);
      rotYVal.textContent = `${deg}°`;
      voxelGroup.rotation.y = THREE.MathUtils.degToRad(deg);
    });

    sliderRotX.addEventListener('input', (e) => {
      const deg = parseInt(e.target.value);
      rotXVal.textContent = `${deg}°`;
      voxelGroup.rotation.x = THREE.MathUtils.degToRad(deg);
    });

    let autoSpin = false;
    btnAutoSpin.addEventListener('click', () => {
      autoSpin = !autoSpin;
      btnAutoSpin.classList.toggle('active', autoSpin);
      btnAutoSpin.textContent = `Auto-Spin: ${autoSpin ? 'ON' : 'OFF'}`;
    });

    btnClear.addEventListener('click', () => {
      const voxelsToRemove = objects.filter(obj => obj !== groundPlane);
      voxelsToRemove.forEach(v => {
        voxelGroup.remove(v);
        v.geometry.dispose();
      });
      objects.length = 1; // เหลือ groundPlane
    });

    // Color Swatch Selection
    document.querySelectorAll('.color-swatch').forEach(swatch => {
      swatch.addEventListener('click', () => {
        document.querySelectorAll('.color-swatch').forEach(s => s.classList.remove('active'));
        swatch.classList.add('active');
        currentColor = parseInt(swatch.dataset.color);
      });
    });

    // 6. Retro CRT TV Channel Carousel
    const tvProjects = [
      {
        title: "CHEMICAL CRASHOUT",
        desc: "Unity Game: ระบบแต่งตัว Safety PPE, เข้าจัดเก็บสารเคมีในห้องแล็บ และเกมเพลย์ Interactive",
        tool: "ENGINE: Unity 3D / C#"
      },
      {
        title: "SPIDER MECH DRONE",
        desc: "Maya 3D Model: การปั้น Hard-surface Mecha, จัดเรียง UV Mapping ตาราง 2D และเท็กซ์เจอร์",
        tool: "SOFTWARE: Autodesk Maya"
      },
      {
        title: "HUMANOID BONE RIG",
        desc: "Character Rigging: ติดตั้งกระดูก IK/FK, Spine Controllers และ Clean up frame animation",
        tool: "SOFTWARE: Maya & Mixamo"
      },
      {
        title: "LEVEL & ENVIRONMENT",
        desc: "Unity Greybox: ออกแบบเส้นทางนำสายตาผู้เล่น พร้อมจัดแสง 3-Point Lighting Studio[cite: 3]",
        tool: "PIPELINE: Blender to Unity"
      }
    ];

    let currentChannel = 0;
    const tvChannelNum = document.getElementById('tvChannelNum');
    const tvProjectTitle = document.getElementById('tvProjectTitle');
    const tvProjectDesc = document.getElementById('tvProjectDesc');
    const tvProjectTool = document.getElementById('tvProjectTool');
    const tvDialNext = document.getElementById('tvDialNext');
    const tvDialPower = document.getElementById('tvDialPower');
    let tvPowerOn = true;

    function updateTVChannel() {
      const p = tvProjects[currentChannel];
      tvChannelNum.textContent = currentChannel + 1;
      tvProjectTitle.textContent = p.title;
      tvProjectDesc.textContent = p.desc;
      tvProjectTool.textContent = p.tool;
    }

    tvDialNext.addEventListener('click', () => {
      if (!tvPowerOn) return;
      currentChannel = (currentChannel + 1) % tvProjects.length;
      updateTVChannel();
    });

    tvDialPower.addEventListener('click', () => {
      tvPowerOn = !tvPowerOn;
      const screen = document.querySelector('.tv-content-frame');
      screen.style.opacity = tvPowerOn ? '1' : '0.1';
    });

    // 7. Animation Loop
    const clock = new THREE.Clock();
    function animate() {
      requestAnimationFrame(animate);
      const delta = clock.getDelta();

      if (autoSpin) {
        voxelGroup.rotation.y += delta * 0.4;
        const deg = Math.round(THREE.MathUtils.radToDeg(voxelGroup.rotation.y) % 360);
        rotYVal.textContent = `${deg}°`;
        sliderRotY.value = deg;
      }

      renderer.render(scene, camera);
    }

    animate();

    window.addEventListener('resize', () => {
      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(window.innerWidth, window.innerHeight);
    });
  </script>
</body>
</html>
        crossorigin="anonymous">
      </a-asset-item>
    </a-assets>

    <a-marker 
      type="pattern" 
      url="https://aitutorialcourse.github.io/tracker.patt"
      smooth="true"
      smoothCount="10"
      smoothTolerance="0.01"
      smoothThreshold="5">
      
      <a-entity
        id="epona-entity"
        gltf-model="#epona-model"
        scale="0.8 0.8 0.8"
        position="0 0 0"
        rotation="0 0 0"
        animation-mixer="clip: *; loop: repeat; crossFadeDuration: 0.4;">
      </a-entity>

      <a-light type="ambient" color="#ffffff" intensity="1.2"></a-light>
      <a-light type="directional" color="#ffffff" intensity="0.8" position="2 4 3"></a-light>
    </a-marker>

    <a-entity camera></a-entity>
  </a-scene>
</body>
</html>
