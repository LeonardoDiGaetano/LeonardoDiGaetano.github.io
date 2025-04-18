---
layout: cv
permalink: /cv/
title: cv
nav: true
nav_order: 4
cv_pdf: example_pdf.pdf
description: This is my CV. Download the pdf for the extended version.
toc:
  sidebar: left
---

<canvas id="network"></canvas>

<style>
  /* 1) allow normal scrolling */
  html, body {
    margin: 0;
    padding: 0;
    width: 100%;
    height: auto;
    background: none;
    overflow: auto;
  }

  /* 2) full‑screen fixed canvas behind everything */
  canvas {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    z-index: -1;
    background-color: #1C1C1D;
  }

  /* 3) override your CV layout’s wrappers to be transparent */
  /*    — replace these selectors with whatever your layout generates */
  .cv-content,
  .cv-wrapper,
  .page,
  .page-content,
  .content-area,
  .toc-sidebar {
    background: transparent !important;
  }

  /* 4) your own content container sits above the canvas */
  #content-container {
    position: relative;
    z-index: 1;
    background: transparent;
    padding: 1.5rem;
    max-width: 800px;
    margin: 2rem auto;
    border-radius: 0.5rem;
  }
</style>

<script>
  document.addEventListener('DOMContentLoaded', () => {
    const canvas = document.getElementById('network');
    const ctx    = canvas.getContext('2d');
    let width, height;
    const mouse = { x: null, y: null };
    const nodes = [];
    const NODE_COUNT         = 100;
    const MAX_DIST           = 100;
    const HIGHLIGHT_RADIUS   = 80;
    const REPULSION_STRENGTH = 0.1;
    const FRICTION           = 0.98;
    const VELOCITY_SCALE     = 0.5;

    function resize() {
      width  = canvas.width  = window.innerWidth;
      height = canvas.height = window.innerHeight;
    }
    window.addEventListener('resize', resize);
    window.addEventListener('mousemove', e => {
      mouse.x = e.clientX;
      mouse.y = e.clientY;
    });

    function init() {
      resize();
      for (let i = 0; i < NODE_COUNT; i++) {
        nodes.push({
          x:  Math.random() * width,
          y:  Math.random() * height,
          vx: (Math.random() - 0.5) * VELOCITY_SCALE,
          vy: (Math.random() - 0.5) * VELOCITY_SCALE
        });
      }
    }

    function dist2(a, b) {
      const dx = a.x - b.x, dy = a.y - b.y;
      return dx*dx + dy*dy;
    }

    function update() {
      ctx.clearRect(0, 0, width, height);

      // 1) fill triangles
      const maxDist2 = MAX_DIST * MAX_DIST;
      ctx.fillStyle = 'rgba(100,150,255,0.1)';
      for (let i = 0; i < NODE_COUNT; i++) {
        for (let j = i+1; j < NODE_COUNT; j++) {
          if (dist2(nodes[i], nodes[j]) > maxDist2) continue;
          for (let k = j+1; k < NODE_COUNT; k++) {
            if (
              dist2(nodes[i], nodes[k]) <= maxDist2 &&
              dist2(nodes[j], nodes[k]) <= maxDist2
            ) {
              ctx.beginPath();
              ctx.moveTo(nodes[i].x, nodes[i].y);
              ctx.lineTo(nodes[j].x, nodes[j].y);
              ctx.lineTo(nodes[k].x, nodes[k].y);
              ctx.closePath();
              ctx.fill();
            }
          }
        }
      }

      // 2) update motion & repulsion
      nodes.forEach(n => {
        if (mouse.x !== null) {
          const dx   = n.x - mouse.x;
          const dy   = n.y - mouse.y;
          const dist = Math.hypot(dx, dy);
          if (dist < MAX_DIST) {
            const force = (MAX_DIST - dist) / MAX_DIST;
            n.vx += (dx/dist) * force * REPULSION_STRENGTH;
            n.vy += (dy/dist) * force * REPULSION_STRENGTH;
          }
        }
        n.vx *= FRICTION;
        n.vy *= FRICTION;
        n.x  += n.vx;
        n.y  += n.vy;
        if (n.x < 0 || n.x > width)  n.vx *= -1;
        if (n.y < 0 || n.y > height) n.vy *= -1;
      });

      // 3) draw edges, highlights, nodes
      for (let i = 0; i < NODE_COUNT; i++) {
        const n = nodes[i];
        for (let j = i+1; j < NODE_COUNT; j++) {
          const m    = nodes[j];
          const dx   = n.x - m.x;
          const dy   = n.y - m.y;
          const dist = Math.hypot(dx, dy);
          if (dist < MAX_DIST) {
            ctx.beginPath();
            ctx.moveTo(n.x, n.y);
            ctx.lineTo(m.x, m.y);
            ctx.strokeStyle = `rgba(255,255,255,${1 - dist/MAX_DIST})`;
            ctx.stroke();
          }
        }
        const dxm = n.x - mouse.x, dym = n.y - mouse.y;
        const dm = mouse.x!==null ? Math.hypot(dxm, dym) : Infinity;
        if (dm < HIGHLIGHT_RADIUS) {
          ctx.beginPath();
          ctx.moveTo(n.x, n.y);
          ctx.lineTo(mouse.x, mouse.y);
          ctx.strokeStyle = `rgba(0,255,255,${1 - dm/HIGHLIGHT_RADIUS})`;
          ctx.stroke();
        }
        ctx.beginPath();
        const r = dm < HIGHLIGHT_RADIUS ? 5 : 2;
        ctx.arc(n.x, n.y, r, 0, Math.PI*2);
        ctx.fillStyle = dm < HIGHLIGHT_RADIUS ? '#0ff' : '#fff';
        ctx.fill();
      }

      requestAnimationFrame(update);
    }

    init();
    update();
  });
</script>

<div id="content-container">
  {% if page.cv_pdf %}
    <object data="{{ page.cv_pdf }}" type="application/pdf" width="100%" height="800">
      Your browser doesn’t support PDFs. <a href="{{ page.cv_pdf }}">Download the PDF</a>.
    </object>
  {% endif %}
  {{ content }}
</div>
