<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>David Aviña | Mechanical Engineer</title>

  <style>
    body {
      margin: 0;
      font-family: Arial, Helvetica, sans-serif;
      background: #f4f6f8;
      color: #1e272e;
    }

    header {
      padding: 40px;
      max-width: 1100px;
      margin: auto;
    }

    h1 {
      color: #1e3799;
      margin-bottom: 10px;
    }

    h2 {
      color: #1e3799;
      margin-top: 40px;
    }

    p {
      line-height: 1.6;
      max-width: 900px;
    }

    #viewer {
      width: 100%;
      height: 600px;
      background: #f4f6f8;
    }

    canvas {
      display: block;
    }
  </style>
</head>

<body>

<header>
  <h1>David Aviña Mechanical Engineer</h1>

  <p>
    I am David Aviña, a Mechanical Engineer with experience in project management and engineering design.
    I have worked on structural and energy-related projects, focused on efficiency, quality, safety,
    and technical problem solving, with a strong interest in continuous improvement, teamwork,
    and delivering reliable engineering solutions worldwide.
  </p>

  <h2>Project Management Experience</h2>

  <p>
    I have led multiple engineering projects as a <strong>Project Manager</strong>, overseeing each
    phase from initial planning to final delivery. In addition to project coordination and technical
    decision-making, I am also responsible for <strong>Engineering Design</strong> and the development
    of fabrication drawings using software such as SolidWorks, AutoCAD, and CATIA, validating accurate
    dimensions for proper manufacturing while ensuring quality, safety, and schedule compliance.
  </p>
</header>

<div id="viewer"></div>

<!-- THREE.JS -->
<script src="https://cdn.jsdelivr.net/npm/three@0.158.0/build/three.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/three@0.158.0/examples/js/controls/OrbitControls.js"></script>
<script src="https://cdn.jsdelivr.net/npm/three@0.158.0/examples/js/loaders/STLLoader.js"></script>

<script>
  const scene = new THREE.Scene();
  scene.background = new THREE.Color(0xf4f6f8);

  const camera = new THREE.PerspectiveCamera(
    60,
    window.innerWidth / 600,
    0.1,
    1000
  );
  camera.position.set(0, 40, 120);

  const renderer = new THREE.WebGLRenderer({ antialias: true });
  renderer.setSize(window.innerWidth, 600);
  document.getElementById("viewer").appendChild(renderer.domElement);

  const controls = new THREE.OrbitControls(camera, renderer.domElement);
  controls.enableDamping = true;

  const light1 = new THREE.DirectionalLight(0xffffff, 1);
  light1.position.set(50, 50, 50);
  scene.add(light1);

  const light2 = new THREE.AmbientLight(0x404040, 1.2);
  scene.add(light2);

  const loader = new THREE.STLLoader();
  loader.load(
    "models/CORE-LOC.stl",
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
      console.error("STL load error:", error);
    }
  );

  window.addEventListener("resize", () => {
    camera.aspect = window.innerWidth / 600;
    camera.updateProjectionMatrix();
    renderer.setSize(window.innerWidth, 600);
  });

  function animate() {
    requestAnimationFrame(animate);
    controls.update();
    renderer.render(scene, camera);
  }

  animate();
</script>

</body>
</html>

