<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Iconic Wears</title>
  <link rel="stylesheet" href="styles.css" />
  <style>
    body {
      margin: 0;
      background: linear-gradient(120deg, #0033cc, #00ccff);
      color: white;
      font-family: 'Segoe UI', sans-serif;
      overflow: hidden;
    }
    .overlay {
      position: absolute;
      top: 20px;
      left: 20px;
      z-index: 1;
    }
    h1 {
      margin: 0;
      font-size: 2.5em;
    }
    p {
      font-size: 1.2em;
    }
    .contact {
      position: absolute;
      bottom: 20px;
      left: 20px;
      font-size: 1em;
    }
    canvas {
      display: block;
    }
    @media (max-width: 600px) {
      h1 {
        font-size: 1.8em;
      }
      p {
        font-size: 1em;
      }
    }
  </style>
</head>
<body>
  <div class="overlay">
    <h1>Iconic Wears</h1>
    <p>We style you the best</p>
    <p><em>Give you the best vibes and wears</em></p>
  </div>
  <div class="contact">
    <p>Contact: 09127702890 | samuelnifemi307@gmail.com</p>
  </div>

  <script type="module">
    import * as THREE from 'https://cdn.jsdelivr.net/npm/three@0.152.2/build/three.module.js';
    import { GLTFLoader } from 'https://cdn.jsdelivr.net/npm/three@0.152.2/examples/jsm/loaders/GLTFLoader.js';

    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(60, window.innerWidth / window.innerHeight, 0.1, 1000);
    camera.position.z = 5;

    const renderer = new THREE.WebGLRenderer({ antialias: true });
    renderer.setSize(window.innerWidth, window.innerHeight);
    document.body.appendChild(renderer.domElement);

    const directionalLight = new THREE.DirectionalLight(0xffffff, 1);
    directionalLight.position.set(2, 2, 5);
    scene.add(directionalLight);

    const ambientLight = new THREE.AmbientLight(0xffffff, 0.5);
    scene.add(ambientLight);

    const loader = new GLTFLoader();
    let model = null;

    const MODEL_URL = 'https://modelviewer.dev/shared-assets/models/Astronaut.glb';

    loader.load(
      MODEL_URL,
      (gltf) => {
        model = gltf.scene;
        model.scale.set(2, 2, 2);
        scene.add(model);
      },
      undefined,
      (error) => {
        console.error('Error loading model:', error);
      }
    );

    function animate() {
      requestAnimationFrame(animate);
      if (model) {
        model.rotation.y += 0.01;
      }
      renderer.render(scene, camera);
    }
    animate();

    window.addEventListener('resize', () => {
      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(window.innerWidth, window.innerHeight);
    });

    window.addEventListener('beforeunload', () => {
      renderer.dispose();
    });
  </script>
</body>
</html>
