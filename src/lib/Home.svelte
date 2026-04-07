<script>
  import { onMount } from "svelte";
  import { link } from "svelte-spa-router";
  import * as THREE from "three";

  let outcome1 = "Heads";
  let outcome2 = "Tails";
  let result = "";

  let container;
  let scene, camera, renderer, coin;
  let animating = false;

  let fadeText = "";
  let showText = false;

  function showFadeText(text) {
    fadeText = text;
    showText = true;
    setTimeout(() => (showText = false), 2000);
  }

  function flipCoin() {
    if (animating) return;
    animating = true;

   // const spins = Math.floor(Math.random() * 6) + 3;
    const spins = Math.floor(Math.random() * 4) + 3;
    const targetRotation = coin.rotation.x + spins * Math.PI;
    const duration = 1800;//2000;
    const start = performance.now();

    function animate(time) {
      const elapsed = time - start;
      const progress = Math.min(elapsed / duration, 1);

      // Base rotation interpolation
      coin.rotation.x = coin.rotation.x + (targetRotation - coin.rotation.x) * progress;

      // Wobble blended into final frames (comment out if undesired)
      //if (progress > 0.8) {
      if (progress > 0.25) {
        const wobble = Math.sin((progress - 0.8) * 6 * Math.PI) * (1 - progress) * 3.6;
        //const wobble = Math.sin((progress - 0.8) * 10 * Math.PI) * (1 - progress) * 0.1;
        coin.rotation.x += wobble;
      }

      renderer.render(scene, camera);

      if (progress < 1) {
        requestAnimationFrame(animate);
      } else {
        animating = false;
        const normalized = coin.rotation.x % (2 * Math.PI);
        if (normalized > Math.PI / 2 && normalized < (3 * Math.PI / 2)) {
          coin.rotation.x = Math.PI; // tails facing camera
          result = outcome2;
        } else {
          coin.rotation.x = 0; // heads facing camera
          result = outcome1;
        }
        showFadeText(result);
      }
    }
    requestAnimationFrame(animate);
  }

  onMount(() => {
    scene = new THREE.Scene();
    camera = new THREE.PerspectiveCamera(
      75,
      container.clientWidth / container.clientHeight,
      0.1,
      1000
    );
    renderer = new THREE.WebGLRenderer({ antialias: true });
    renderer.setSize(container.clientWidth, container.clientHeight);
    container.appendChild(renderer.domElement);

    const loader = new THREE.TextureLoader();
    const headsTexture = loader.load("/heads.svg");
    const tailsTexture = loader.load("/tails.svg");

    const geometry = new THREE.CylinderGeometry(1, 1, 0.1, 64);
    //const materialSide = new THREE.MeshBasicMaterial({ color: 0x999999 });
    const materialSide = new THREE.MeshBasicMaterial({ color: 0x999900 });
    const materialHeads = new THREE.MeshBasicMaterial({ map: headsTexture });
    const materialTails = new THREE.MeshBasicMaterial({ map: tailsTexture });

    // CylinderGeometry uses [side, side, top, bottom] order
    const materials = [materialSide, materialSide, materialHeads, materialTails];
    coin = new THREE.Mesh(geometry, materials);
    scene.add(coin);

    camera.position.z = 5;
    renderer.render(scene, camera);

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
  .coin-wrapper {
    position: relative;
    background: #111;

  }
  .coin {
    width: 100%;
    height: 100%;
  }
  .fade-text {
    position: absolute;
    top: 38%;
    left: 50%;
    transform: translateX(-50%);
    font-size: 2rem;
    font-family: Arial, Helvetica, sans-serif;
    color: whitesmoke;
    opacity: 0;
    animation: fadeUp 2s forwards;
    pointer-events: none;
    z-index: 300;
  }
  @keyframes fadeUp {
    0% {
      opacity: 0;
      transform: translate(-50%, 0);
    }
    50% {
      opacity: 1;
      transform: translate(-50%, -20px);
    }
    100% {
      opacity: 0;
      transform: translate(-50%, -40px);
    }
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
  .info-span {
    font-size: small;
    font-family: Arial, Helvetica, sans-serif;
    position: absolute;
    top: 3%;
    left: 30%;
    color: plum;
  }

  @media (max-width: 768px) {
    .layout {
      grid-template-columns: 1fr;
      grid-template-rows: auto auto;

      width: 324px;
    }
    .coin-wrapper {
        height: 60vh;
        min-width: 340px;
        background-color: black;
        left: 3%;
    }
    .info-span {
        left: 10%;
        top: 86%;
    }
    input {
      width: 280px;
    }
    /* .nav-div {
      top: 2%;
      left: 15%;
    } */
  }
</style>

<div class="layout">
  <div class="coin-wrapper">
    <span class="info-span">Tap the screen or swipe the coin to flip</span>
    <div class="coin" bind:this={container}></div>
    {#if showText}
      <div class="fade-text">{fadeText}</div>
    {/if}
  </div>
  
  <div class="inputs">
   <!-- <div class="nav-div">
    <a href="/about" use:link>About</a>
    <a href="/learn" use:link>Learn</a>
   </div> -->
    <label for="heads">Heads outcome:</label>
    <input bind:value={outcome1} id="heads"/>
    <label for="tails">Tails outcome:</label>
    <input bind:value={outcome2} id="tails"/>
    <div class="result">
        <img src="/coin-logo.svg" alt="coin-flip" width="48" height="48" />
        Result: {result}
    </div>
    <div style="margin: 8px;padding: 6px">
        <img src="/sign-warn.svg" alt="disclaimer" width="16" height="16" />
        <span style="font-size: xx-small;">Disclaimer: Do not base serious, life-decisions on a coin flip.</span>
    </div>
    <a href="/policy" style="font-size: small;" use:link>Terms & Conditions</a>
  </div>
</div>
