<script lang="ts">
  import { onMount, onDestroy } from 'svelte';
  
  // Constants
  const spacing = 30;
  const baseRadius = 1.5;
  const hoverRadius = 4;
  const baseColor = '#1F75FE';
  const trailRadius = spacing * 3;

  // Canvas and context - only canvas needs to be reactive for binding
  let canvas = $state<HTMLCanvasElement>();
  let ctx: CanvasRenderingContext2D | null = null;
  
  // Performance-critical data - keep as regular variables to avoid reactive overhead
  let grid: Array<{
    x: number;
    y: number;
    glow: boolean;
    glowTimer: number;
  }> = [];
  let cols = 0;
  let rows = 0;
  let mouse = { x: -9999, y: -9999 };
  let animationId: number | null = null;

  // Event cleanup functions
  let cleanupFunctions: Array<() => void> = [];

  function resizeCanvas() {
    if (!canvas || !ctx) return;
    
    const dpr = window.devicePixelRatio || 1;
    const width = window.innerWidth;
    const height = Math.max(document.body.scrollHeight, window.innerHeight);

    canvas.width = width * dpr;
    canvas.height = height * dpr;
    canvas.style.width = width + 'px';
    canvas.style.height = height + 'px';

    ctx.setTransform(1, 0, 0, 1, 0, 0);
    ctx.scale(dpr, dpr);

    cols = Math.floor(width / spacing);
    rows = Math.floor(height / spacing);
    generateGrid();
  }

  function generateGrid() {
    grid = [];
    for (let y = 0; y <= rows; y++) {
      for (let x = 0; x <= cols; x++) {
        grid.push({
          x: x * spacing,
          y: y * spacing,
          glow: false,
          glowTimer: Math.floor(Math.random() * 600) + 300
        });
      }
    }
  }

  function handleMouseMove(e: MouseEvent) {
    mouse.x = e.clientX;
    mouse.y = e.clientY;
    
    // Handle custom cursor in the same function to avoid duplicate event processing
    const cursor = document.querySelector('.custom-cursor') as HTMLElement;
    if (cursor) {
      const scrollY = window.scrollY || window.pageYOffset;
      cursor.style.left = e.clientX + 'px';
      cursor.style.top = (e.clientY + scrollY) + 'px';
    }
  }

  function draw() {
    if (!ctx || !canvas) return;
    
    ctx.clearRect(0, 0, canvas.width, canvas.height);

    const scrollY = window.scrollY || window.pageYOffset;

    for (let dot of grid) {
      const dist = Math.hypot(dot.x - mouse.x, dot.y - (mouse.y + scrollY));
      let r = baseRadius;
      let opacity = 0.15;

      if (dist < trailRadius) {
        const t = dist / trailRadius;
        const level = 1 - t;
        r = baseRadius + (hoverRadius - baseRadius) * level;
        opacity = 0.15 + 0.85 * level;
      } else {
        dot.glowTimer--;

        if (dot.glowTimer <= 0) {
          dot.glow = !dot.glow;
          dot.glowTimer = dot.glow
            ? Math.floor(Math.random() * 60) + 120
            : Math.floor(Math.random() * 500) + 300;
        }

        if (dot.glow) {
          opacity = 0.3;
          r = baseRadius + 0.3;
        }
      }

      ctx.beginPath();
      ctx.arc(dot.x, dot.y, r, 0, Math.PI * 2);
      ctx.fillStyle = `rgba(31, 117, 254, ${opacity})`;
      ctx.fill();
    }

    animationId = requestAnimationFrame(draw);
  }

  onMount(() => {
    if (canvas) {
      ctx = canvas.getContext('2d');
      
      // Set up event listeners with cleanup
      const resizeHandler = () => resizeCanvas();
      const mouseMoveHandler = (e: MouseEvent) => handleMouseMove(e);
      
      window.addEventListener('resize', resizeHandler);
      window.addEventListener('mousemove', mouseMoveHandler);
      
      // Store cleanup functions
      cleanupFunctions.push(
        () => window.removeEventListener('resize', resizeHandler),
        () => window.removeEventListener('mousemove', mouseMoveHandler)
      );
      
      // Initialize
      resizeCanvas();
      draw();
    }
  });

  onDestroy(() => {
    // Clean up event listeners
    cleanupFunctions.forEach(cleanup => cleanup());
    
    // Cancel animation frame
    if (animationId !== null) {
      cancelAnimationFrame(animationId);
    }
  });
</script>

<canvas bind:this={canvas} id="dotCanvas" style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; z-index: -1; pointer-events: none;"></canvas>