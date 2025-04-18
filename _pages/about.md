---
layout: about
title: about
permalink: /
subtitle:

profile:
  align: right
  image: prof_pic.jpg
  image_circular: true # crops the image to make it circular
  more_info: >


news: true  # includes a list of news items
latest_posts: true  # includes a list of the newest posts
selected_papers: true # includes a list of papers marked as "selected={true}"
social: true  # includes social icons at the bottom of the page
---

<!-- Canvas di sfondo dinamico -->
<canvas id="network"></canvas>

<style>
  /* Sfondo e canvas */
  html, body {
    margin: 0;
    padding: 0;
    overflow: hidden;
    background-color: #000;
  }
  #network {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: -1;
    display: block;
  }
</style>

<script>
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

    function update() {
      ctx.clearRect(0, 0, width, height);
      nodes.forEach(n => {
        // repulsione dal mouse
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
        // smorzamento
        n.vx *= FRICTION;
        n.vy *= FRICTION;
        // spostamento
        n.x += n.vx;
        n.y += n.vy;
        if (n.x < 0 || n.x > width) n.vx *= -1;
        if (n.y < 0 || n.y > height) n.vy *= -1;
      });
      // disegna connessioni e nodi
      for (let i = 0; i < nodes.length; i++) {
        const n = nodes[i];
        // connessioni
        for (let j = i + 1; j < nodes.length; j++) {
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
        // evidenziazione verso il mouse
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
        // nodo
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
</script>

I am a postdoctoral researcher with dual affiliations at the [Institut de Neurosciences de la Timone](https://www.int.univ-amu.fr/) and the [Centre de Physique Théorique, Aix-Marseille Université](https://www.cpt.univ-mrs.fr/). My research lies at the intersection of network science and neuroscience, with a strong focus on the theoretical foundations of network science and their application to understanding the organization and dynamics of brain networks.

I earned my PhD in [Network and Data Science](https://networkdatascience.ceu.edu/) at [Central European University](https://www.ceu.edu/), under the supervision of [Federico Battiston](https://scholar.google.com/citations?hl=it&user=aDf1nroAAAAJ&view_op=list_works&sortby=pubdate), with [Michele Starnini](https://scholar.google.com/citations?user=duBif0oAAAAJ&hl=en) as an external advisor.
