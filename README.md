# David Aviña Mechanical Engineer
I am David Aviña, a Mechanical Engineer with experience in project management and engineering design. I have worked on structural and energy-related projects, focused on efficiency, quality, safety, and technical problem solving, with a strong interest in continuous improvement, teamwork, and delivering reliable engineering solutions worldwide.
## Project Management Experience

I have led multiple engineering projects as a **Project Manager**, overseeing each phase from initial planning to final delivery. In addition to project coordination and technical decision-making, I am also responsible for **Engineering Design** and the development of fabrication drawings using software such as SolidWorks, AutoCAD, and CATIA, validating accurate dimensions for proper manufacturing while ensuring quality, safety, and schedule compliance.

---

### 📌 Project Planning & Scope Definition
![Project Planning](images/planning.jpg)

- Defined project scope, objectives, and deliverables  
- Created schedules, budgets, and risk assessments  
- Coordinated with stakeholders and engineering teams  

---

### 📐 Design & Engineering Phase
![Design Phase](images/design.jpg)

- Supervised structural and mechanical design development  
- Reviewed technical drawings and calculations  
- Ensured compliance with engineering standards and client requirements  

---

### 🏗️ Execution & Construction
![Execution](images/execution.jpg)

- Managed on-site activities and contractor coordination  
- Monitored progress, quality, and safety  
- Solved technical issues during construction  

---

### ✅ Project Closure & Delivery
![Delivery](images/delivery.jpg)

- Verified final deliverables and documentation  
- Ensured client satisfaction and handover  
- Evaluated lessons learned for continuous improvement

- <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>CORE-LOC 3D Viewer</title>
  <style>
    body {
      margin: 0;
      background: #f4f6f8;
      overflow: hidden;
    }
    canvas {
      display: block;
    }
  </style>
</head>
<body>

<script src="https://cdn.jsdelivr.net/npm/three@0.158.0/build/three.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/three@0.158.0/examples/js/controls/OrbitControls.js"></script>
<script src="https://cdn.jsdelivr.net/npm/three@0.158.0/examples/js/loaders/STLLoader.js"></script>

<script>
  // Scene
  const scene = new THREE.Scene();
  scene.background = new THREE.Color(0xf4f6f8);

  // Camera
  const camera = new THREE.PerspectiveCamera(
    60,
    window.innerWidth / window.innerHeight,
    0.1,
    1000
  );
  camera.position.set(0, 40, 100);

  // Renderer
  const renderer = new THREE.WebGLRenderer({ antialias: true });
  renderer.setSize(window.innerWidth, window.innerHeight);
  document.body.appendChild(renderer.domElement);

  // Controls
  const controls = new THREE.OrbitControls(camera, renderer.domElement);
  controls.enableDamping = true;

  // Lights
  const directionalLight = new THREE.DirectionalLight(0xffffff, 1);
  directionalLight.position.set(50, 50, 50);
  scene.add(directionalLight);

  const ambientLight = new THREE.AmbientLight(0x404040, 1.2);
  scene.add(ambientLight);

  // Load STL
  const loader = new THREE.STLLoader();
  loader.load(
    'models/CORE-LOC.stl',
    function (geometry) {
      geometry.center();

      const material = new THREE.MeshStandardMaterial({
        color: 0x1e3799,
        metalness: 0.35,
        roughness: 0.45
      });

      const mesh = new THREE.Mesh(geometry, material);
      scene.add(mesh);
    },
    undefined,
    function (error) {
      console.error('Error loading STL:', error);
    }
  );

  // Resize
  window.addEventListener('resize', () => {
    camera.aspect = window.innerWidth / window.innerHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(window.innerWidth, window.innerHeight);
  });

  // Animate
  function animate() {
    requestAnimationFrame(animate);
    controls.update();
    renderer.render(scene, camera);
  }
  animate();
</script>

</body>
</html>

