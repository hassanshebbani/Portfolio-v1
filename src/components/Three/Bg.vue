<script setup lang="ts">
import { ref, onMounted, watch } from "vue";
import gsap from "gsap";
import * as THREE from "three";
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls";
const myCanvas = ref<HTMLCanvasElement>();

const props = defineProps({
  animateCanvas: Number,
});

const cameraGroup = new THREE.Group();
const parameters = {
  materialColor: "#00ffff",
};
const scene = new THREE.Scene();
// 19 22
const sphereGeometry = new THREE.SphereBufferGeometry(1, 32, 32);
const torusGeo = new THREE.TorusBufferGeometry(1,1.1, 80, 32, 12);
const torusKnotGeo = new THREE.TorusKnotBufferGeometry(0.2, 0.5, 51, 10, 74, 3);
const pointsMaterial = new THREE.PointsMaterial({
    
  color: parameters.materialColor,
  size: 0.01,
  sizeAttenuation: true,
  transparent: true,
  // vertexColors: true,
});
const pointsMaterialRed = new THREE.PointsMaterial({
    
  color: "red",
  size: 0.01,
  sizeAttenuation: true,
  transparent: true,
  // vertexColors: true,
});
const sphereParticles = new THREE.Points(sphereGeometry, pointsMaterial);
const torusParticles = new THREE.Points(torusGeo, pointsMaterial);
const torusKnotParticles = new THREE.Points(torusKnotGeo, pointsMaterial);
const material = new THREE.MeshBasicMaterial({
  color: parameters.materialColor,
  wireframe: true,
});

const animateCanvas = () => {
  const mesh = new THREE.Mesh(torusGeo, material);
  mesh.position.x = 2
    torusParticles.material.opacity = 0.15;
//   scene.add(mesh);
  scene.add(sphereParticles, torusParticles);
//   scene.add(torusParticles, sphereParticles);

  // Particles
  const particleCount = 100;
  const positions = new Float32Array(particleCount * 3);
  const particlesMaterial = new THREE.PointsMaterial({
    color: parameters.materialColor,
    size: 0.02,
    sizeAttenuation: true,
  });
  for (let i = 0; i < particleCount; i++) {
    const i3 = i * 3;
    const particlesGeometry = new THREE.BufferGeometry();
    positions[i3 + 0] = (Math.random() - 0.5) * 10;
    positions[i3 + 1] = (Math.random() - 0.5) * 10;
    positions[i3 + 2] = (Math.random() - 0.5) * 10;

    particlesGeometry.setAttribute(
      "position",
      new THREE.BufferAttribute(positions, 3)
    );
    const points = new THREE.Points(particlesGeometry, particlesMaterial);
    scene.add(points);
  }
  const sizes = {
    width: window.innerWidth,
    height: window.innerHeight,
  };

  // Base camera

  scene.add(cameraGroup);
  const camera = new THREE.PerspectiveCamera(
    35,
    sizes.width / sizes.height,
    0.1,
    100
  );
  camera.position.z = 3;
  cameraGroup.add(camera);

  const renderer = new THREE.WebGLRenderer({
    canvas: myCanvas.value,
    alpha: true,
  });
  // renderer.setClearAlpha(1)
  renderer.setSize(sizes.width, sizes.height);
  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));

  const clock = new THREE.Clock();
  let previousTime = 0;

  // Todo: Scrolling the camera
  let scrollY = window.scrollY;

  const cursor = {
    x: 0,
    y: 0,
  };

  const controls = new OrbitControls(camera, myCanvas.value);
  controls.enableDamping = true;
  controls.enableZoom = false;

  const tick = () => {
    const elapsedTime = clock.getElapsedTime();
    const deltaTime = elapsedTime - previousTime;
    previousTime = elapsedTime;

    camera.position.y = -scrollY / sizes.height;

    // Parallax
    const parallaxX = cursor.x * 6;
    const parallaxY = cursor.y * 6;
    cameraGroup.position.x +=
      (parallaxX - cameraGroup.position.x) * 5 * deltaTime;
    cameraGroup.position.y -=
      (parallaxY + cameraGroup.position.y) * 5 * deltaTime;
    sphereParticles.rotation.x = 0.05 * elapsedTime;
    sphereParticles.rotation.y = 0.05 * elapsedTime;
    torusParticles.rotation.x = 0.05 * elapsedTime;
    torusParticles.rotation.y = 0.05 * elapsedTime;
    controls.update();
    // Render
    renderer.render(scene, camera);
    window.requestAnimationFrame(tick);
  };

  tick();

  // Dat Gui

  // Todo: Parallax effect using mousemove & the cursor
  window.addEventListener("mousemove", (e) => {
    cursor.x = e.clientX / sizes.width - 0.5;
    cursor.y = e.clientY / sizes.height - 0.5;
  });

  window.addEventListener("resize", () => {
    sizes.width = window.innerWidth;
    sizes.height = window.innerHeight;
    camera.aspect = sizes.width / sizes.height;
    camera.updateProjectionMatrix();
    renderer.setSize(sizes.width, sizes.height);
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
  });
  interface Document {
    exitFullscreen: any;
    mozCancelFullScreen: any;
    webkitExitFullscreen: any;
    fullscreenElement: any;
    mozFullScreenElement: any;
    webkitFullscreenElement: any;
    webkitRequestFullscreen: any;
    requestFullscreen: any;
  }
  interface HTMLCanvasElement extends Document {}
  window.addEventListener("dblclick", () => {
    const c = myCanvas.value! as unknown as HTMLCanvasElement;
    const d = myCanvas.value! as unknown as Document;
    const fullScreenElement =
      document.fullscreenElement || d.webkitFullscreenElement;
    if (!fullScreenElement) {
      if (c.requestFullscreen) myCanvas.value!.requestFullscreen();
      else if (c.webkitFullscreenElement) c.webkitRequestFullscreen();
    } else {
      if (document.exitFullscreen) document.exitFullscreen();
      else if (d.webkitExitFullscreen) d.webkitExitFullscreen();
    }
  });
  const s = () => {
    if (cameraGroup.position.z <= -6) {
      cameraGroup.position.z = 0;
    }
    gsap.to(cameraGroup.rotation, {
      duration: 2,
      y: "-=2",
      ease: "power2.inOut",
    });
    gsap.to(cameraGroup.position, {
      duration: 2,
      z: "-=2",
      ease: "power2.inOut",
    });
  };
  watch(props, () => {
    s();
  });
};
onMounted(async () => {
  animateCanvas();
});
</script>

<template>
  <canvas class="webgl fixed top-0 left-0" ref="myCanvas"></canvas>
</template>

<style lang="scss" scoped></style>
