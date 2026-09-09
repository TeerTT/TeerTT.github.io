<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, user-scalable=no, minimum-scale=1.0, maximum-scale=1.0" />
  <title>AR.js Animation Model Viewer</title>

  <!-- A-Frame Library -->
  <script src="https://aframe.io/releases/1.4.2/aframe.min.js"></script>

  <!-- AR.js for A-Frame -->
  <script src="https://raw.githack.com/AR-js-org/AR.js/master/aframe/build/aframe-ar.js"></script>

  <!-- aframe-extras (สำหรับเล่น Animation ของไฟล์ glTF / glb) -->
  <script src="https://cdn.jsdelivr.net/gh/c-frame/aframe-extras@7.2.0/dist/aframe-extras.min.js"></script>

  <style>
    body {
      margin: 0;
      overflow: hidden;
    }
    #ui-guide {
      position: fixed;
      top: 16px;
      left: 50%;
      transform: translateX(-50%);
      z-index: 9999;
      background: rgba(0, 0, 0, 0.75);
      color: #ffffff;
      padding: 8px 16px;
      border-radius: 20px;
      font-family: sans-serif;
      font-size: 14px;
      pointer-events: none;
      text-align: center;
      box-shadow: 0 4px 10px rgba(0,0,0,0.3);
    }
  </style>
</head>
<body>
  <!-- UI แนะนำผู้ใช้ -->
  <div id="ui-guide">📷 ส่องกล้องไปที่ Marker เพื่อแสดงโมเดล 3D</div>

  <!-- A-Frame Scene สำหรับรัน AR.js -->
  <a-scene
    embedded
    arjs="sourceType: webcam; debugUIEnabled: false; detectionMode: mono_and_matrix; matrixCodeType: 3x3;"
    renderer="logarithmicDepthBuffer: true; colorManagement: true;"
    vr-mode-ui="enabled: false">

    <!-- กำหนด Asset ล่วงหน้า -->
    <a-assets>
      <a-asset-item 
        id="eponaModel" 
        src="https://sibsansuk.github.io/epona.glb" 
        crossorigin="anonymous">
      </a-asset-item>
    </a-assets>

    <!-- Marker: กำหนด Pattern หรือใช้ Preset เป็น Hiro หรือ Custom Pattern -->
    <!-- 
      หมายเหตุ: สำหรับรูปภาพ Custom Marker (tracker.png) ปกติจะต้องนำไปแปลงเป็นไฟล์ .patt ผ่าน 
      AR.js Marker Training ก่อน (https://jeromeetienne.github.io/AR.js/three.js/examples/marker-training/examples/generator.html)
      ในตัวอย่างนี้ตั้งค่าแบบ Custom Pattern ไว้ พร้อม Fallback ใช้ Preset 'hiro' สำรอง
    -->
    <a-marker type="pattern" url="https://aitutorialcourse.github.io/tracker.patt">
      
      <!-- โมเดล 3D พร้อมสั่ง animation-mixer ให้เล่นแอนิเมชันวนซ้ำ (loop: repeat) -->
      <a-entity
        id="modelEntity"
        gltf-model="#eponaModel"
        scale="0.8 0.8 0.8"
        position="0 0 0"
        rotation="0 0 0"
        animation-mixer="clip: *; loop: repeat;">
      </a-entity>

      <!-- แสงช่วยส่องโมเดลให้มีมิติคมชัดขึ้น -->
      <a-light type="ambient" color="#ffffff" intensity="1.2"></a-light>
      <a-light type="directional" color="#ffffff" intensity="0.8" position="1 4 2"></a-light>
    </a-marker>

    <!-- กล้อง AR -->
    <a-entity camera></a-entity>
  </a-scene>
</body>
</html>
