---
layout: about
title: about
permalink: /
subtitle:

profile:
  align: right
  image: prof_pic.jpg
  image_circular: true
  more_info: >

news: true
latest_posts: true
selected_papers: true
social: true
---

<canvas id="network"></canvas>

<style>
  html, body {
    margin: 0;
    padding: 0;
    height: 100%;
    width: 100%;
    background: none;
    overflow: hidden;
  }
  canvas {
    position: fixed;
    top: 0;
    left: 0;
    z-index: -1;
    display: block;
    background-color: #1C1C1D;
  }
  #content-container {
    position: relative;
    z-index: 1;
    background-color: rgba(0, 0, 0, 0);
    padding: 1.5rem;
    border-radius: 0.5rem;
    max-width: 800px;
    margin: 2rem auto;
  }
  /* Nasconde il canvas su schermi piccoli */
  @media (max-width: 800px) {
    #network {
      display: none !important;
    }
    html, body {
      overflow: auto;
    }
  }
</style>

<script>
  if (window.innerWidth > 800) {
    document.addEventListener('DOMContentLoaded', () => {
      const canvas = document.getElementById('network');
      const ctx = canvas.getContext('2d');
      let width, height;
      const mouse = { x: null, y: null };
      const nodes = [];
      const NODE_COUNT = 100;
      const MAX_DIST = 100;
      const HIGHLIGHT_RADIUS = 80;
      const REPULSION_STRENGTH = 0.1;
      const FRICTION = 0.98;
      const VELOCITY_SCALE = 0.5;

      function resize() {
        width = canvas.width = window.innerWidth;
        height = canvas.height = window.innerHeight;
      }
      window.addEventListener('resize', resize);
      window.addEventListener('mousemove', e => {
        mouse.x = e.clientX;
        mouse.y = e.clientY;
      });

      function init() {
        resize();
        nodes.length = 0;
        for (let i = 0; i < NODE_COUNT; i++) {
          nodes.push({
            x: Math.random() * width,
            y: Math.random() * height,
            vx: (Math.random() - 0.5) * VELOCITY_SCALE,
            vy: (Math.random() - 0.5) * VELOCITY_SCALE
          });
        }
      }

      function dist2(a, b) {
        const dx = a.x - b.x;
        const dy = a.y - b.y;
        return dx * dx + dy * dy;
      }

      function update() {
        ctx.clearRect(0, 0, width, height);

        // 1) fill triangles
        const maxDist2 = MAX_DIST * MAX_DIST;
        ctx.fillStyle = 'rgba(100,150,255,0.1)';
        for (let i = 0; i < NODE_COUNT; i++) {
          for (let j = i + 1; j < NODE_COUNT; j++) {
            if (dist2(nodes[i], nodes[j]) > maxDist2) continue;
            for (let k = j + 1; k < NODE_COUNT; k++) {
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
            const dx = n.x - mouse.x;
            const dy = n.y - mouse.y;
            const dist = Math.hypot(dx, dy);
            if (dist < MAX_DIST) {
              const force = (MAX_DIST - dist) / MAX_DIST;
              n.vx += (dx / dist) * force * REPULSION_STRENGTH;
              n.vy += (dy / dist) * force * REPULSION_STRENGTH;
            }
          }
          n.vx *= FRICTION;
          n.vy *= FRICTION;
          n.x += n.vx;
          n.y += n.vy;
          if (n.x < 0 || n.x > width)  n.vx *= -1;
          if (n.y < 0 || n.y > height) n.vy *= -1;
        });

        // 3) draw edges, highlights, nodes
        for (let i = 0; i < NODE_COUNT; i++) {
          const n = nodes[i];

          // edges
          for (let j = i + 1; j < NODE_COUNT; j++) {
            const m = nodes[j];
            const dx = n.x - m.x;
            const dy = n.y - m.y;
            const dist = Math.hypot(dx, dy);
            if (dist < MAX_DIST) {
              ctx.beginPath();
              ctx.moveTo(n.x, n.y);
              ctx.lineTo(m.x, m.y);
              ctx.strokeStyle = `rgba(255,255,255,${1 - dist / MAX_DIST})`;
              ctx.stroke();
            }
          }

          // mouse highlight
          const dxm = n.x - mouse.x;
          const dym = n.y - mouse.y;
          const distMouse = mouse.x !== null ? Math.hypot(dxm, dym) : Infinity;
          if (distMouse < HIGHLIGHT_RADIUS) {
            ctx.beginPath();
            ctx.moveTo(n.x, n.y);
            ctx.lineTo(mouse.x, mouse.y);
            ctx.strokeStyle = `rgba(0,255,255,${1 - distMouse / HIGHLIGHT_RADIUS})`;
            ctx.stroke();
          }

          // node
          ctx.beginPath();
          const r = distMouse < HIGHLIGHT_RADIUS ? 5 : 2;
          ctx.arc(n.x, n.y, r, 0, Math.PI * 2);
          ctx.fillStyle = distMouse < HIGHLIGHT_RADIUS ? '#0ff' : '#fff';
          ctx.fill();
        }

        requestAnimationFrame(update);
      }

      init();
      update();
    });
  }
</script>

<div id="content-container">
  <p>
    I am a postdoctoral researcher with dual affiliations at the
    <a href="https://www.int.univ-amu.fr/">Institut de Neurosciences de la Timone</a>
    and the
    <a href="https://www.cpt.univ-mrs.fr/">Centre de Physique Théorique, Aix‑Marseille Université</a>,
    supervised by
    <a href="https://scholar.google.com/citations?user=vsskO0AAAAAJ&hl=it&oi=ao">Andrea Brovelli</a>
    and
    <a href="https://scholar.google.com/citations?hl=it&user=5MeSMfAAAAAJ">Alain Barrat</a>.
  </p>
  <p>
    My research lies at the intersection of network science and neuroscience, with a strong focus on the theoretical foundations of network science and their application to understanding the organization and dynamics of brain networks.
  </p>
  <p>
    I earned my PhD in
    <a href="https://networkdatascience.ceu.edu/">Network and Data Science</a>
    at
    <a href="https://www.ceu.edu/">Central European University</a>,
    under the supervision of
    <a href="https://scholar.google.com/citations?hl=it&user=aDf1nroAAAAJ&view_op=list_works&sortby=pubdate">Federico Battiston</a>,
    with
    <a href="https://scholar.google.com/citations?user=duBif0oAAAAJ&hl=en">Michele Starnini</a>
    as an external advisor.
  </p>