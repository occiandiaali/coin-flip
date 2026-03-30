<script>
  import { onMount } from "svelte";
  import * as THREE from "three";

  let outcome1 = "Heads outcome";
  let outcome2 = "Tails outcome";
  let result = "";

  let container;

  let scene, camera, renderer, coin, animating = false;

  function flipCoin() {
    if (animating) return;
    animating = true;

    // Randomize spins
    const spins = Math.floor(Math.random() * 4) + 3;
    const targetRotation = coin.rotation.x + spins * Math.PI;

    const duration = 2000;
    const start = performance.now();

    function animate(time) {
      const elapsed = time - start;
      const progress = Math.min(elapsed / duration, 1);
      coin.rotation.x = coin.rotation.x + (targetRotation - coin.rotation.x) * progress;

      renderer.render(scene, camera);

      if (progress < 1) {
        requestAnimationFrame(animate);
      } else {
        animating = false;
        // Decide outcome
        const normalized = coin.rotation.x % (2 * Math.PI);
        if (normalized > Math.PI / 2 && normalized < (3 * Math.PI / 2)) {
          result = outcome2; // tails
        } else {
          result = outcome1; // heads
        }
      }
    }
    requestAnimationFrame(animate);
  }

  onMount(() => {
    scene = new THREE.Scene();
    camera = new THREE.PerspectiveCamera(75, container.clientWidth / container.clientHeight, 0.1, 1000);
    renderer = new THREE.WebGLRenderer({ antialias: true });
    renderer.setSize(container.clientWidth, container.clientHeight);
    container.appendChild(renderer.domElement);

    const geometry = new THREE.CylinderGeometry(1, 1, 0.1, 64);
    const materialHeads = new THREE.MeshBasicMaterial({ color: 0xffd700 });
    const materialTails = new THREE.MeshBasicMaterial({ color: 0xcccccc });
    const materials = [materialHeads, materialTails, materialHeads];
    coin = new THREE.Mesh(geometry, materials);
    scene.add(coin);

    camera.position.z = 5;

    renderer.render(scene, camera);

    // Swipe / click
    renderer.domElement.addEventListener("click", flipCoin);
    renderer.domElement.addEventListener("touchstart", flipCoin);
  });
</script>

<style>
  .layout {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1rem;
    height: 100vh;
  }
  .coin {
    background: #111;
  }
  .inputs {
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 1rem;
  }
  input {
    margin-bottom: 1rem;
    padding: 0.5rem;
    font-size: 1rem;
  }
  .result {
    margin-top: 1rem;
    font-weight: bold;
    font-size: 1.2rem;
  }
  @media (max-width: 600px) {
    .layout {
      width: 325px;  
      grid-template-columns: 1fr;
      grid-template-rows: auto auto;
    }
  }
</style>

<div class="layout">
  <div class="coin" bind:this={container}></div>
  <div class="inputs">
    <label for="heads">Heads outcome:</label>
    <input bind:value={outcome1} id="heads" />
    <label for="tails">Tails outcome:</label>
    <input bind:value={outcome2} id="tails"/>
    <div class="result">Result: {result}</div>
  </div>
</div>
