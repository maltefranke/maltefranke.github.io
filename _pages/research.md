---
layout: page
permalink: /research/
title: Research
description: research interests and ongoing projects.
nav: true
nav_order: 2
---

## Generative models for chemistry

How can we design molecules with desired property profiles? How can we explore the vast chemical space efficiently?

My first project in my PhD introduced Morph, a flexible-size 3D generative model for molecules. Morph lifts the arbitrary fixed-size or directional constraints that current 3D generative models face by allowing multiple insertions, deletions and substitutions of atoms. 

<div id="morph-pair" style="display:flex; gap:1rem; align-items:center; justify-content:center; visibility:hidden;">
  <iframe
    id="morph-viewer"
    src="{{ '/assets/html/morph_trajectory.html' | relative_url }}"
    width="480"
    height="360"
    style="border:0; background:#1c1c1d; flex:0 0 auto;"
    title="Molecular morph trajectory">
  </iframe>
  <img
    id="morph-gif"
    data-src="{{ '/assets/gifs/morph_trajectory.gif' | relative_url }}"
    alt="Atom count along the morph trajectory"
    style="height:360px; width:auto; flex:0 0 auto;" />
</div>
<script>
(function () {
  const container = document.getElementById("morph-pair");
  const iframe = document.getElementById("morph-viewer");
  const img = document.getElementById("morph-gif");
  const gifSrc = img.dataset.src;
  let viewerReady = false;
  let gifReady = false;

  function start() {
    if (!viewerReady || !gifReady) return;
    requestAnimationFrame(() => {
      // Epoch-based anchor so the iframe can convert via its own timeOrigin.
      const startTime = performance.now() + performance.timeOrigin;
      img.src = gifSrc;
      iframe.contentWindow.postMessage({type: "morph-start", startTime}, "*");
      container.style.visibility = "visible";
    });
  }

  window.addEventListener("message", (e) => {
    if (e.source === iframe.contentWindow && e.data && e.data.type === "morph-ready") {
      viewerReady = true;
      start();
    }
  });

  const preload = new Image();
  preload.onload = () => { gifReady = true; start(); };
  preload.onerror = () => { gifReady = true; start(); };
  preload.src = gifSrc;
})();
</script>
