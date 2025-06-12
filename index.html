import { useEffect, useRef } from "react";

export default function KeyboardPong() {
  const canvasRef = useRef(null);

  useEffect(() => {
    const canvas = canvasRef.current;
    const ctx = canvas.getContext("2d");

    // ─────────────────── Resize handling ───────────────────
    const resize = () => {
      canvas.width = Math.min(window.innerWidth * 0.9, 900);
      canvas.height = Math.min(window.innerHeight * 0.7, 600);
    };
    resize();
    window.addEventListener("resize", resize);

    // ─────────────────── Constants ───────────────────
    const PADDLE_WIDTH = 100;
    const PADDLE_HEIGHT = 12;
    const BALL_RADIUS = 8;
    const PLAYER_MOVE_DURATION = 100; // ms (0.1 s)
    const SPEED_MULTIPLIER = 1.2;

    // ─────────────────── Game objects ───────────────────
    const player = {
      x: canvas.width / 2,
      y: canvas.height - PADDLE_HEIGHT * 2,
      w: PADDLE_WIDTH,
      h: PADDLE_HEIGHT,
      // Anim fields
      targetX: null,
      targetY: null,
      startX: null,
      startY: null,
      moveStart: 0,
    };

    const ai = { x: canvas.width / 2, y: PADDLE_HEIGHT * 2, w: PADDLE_WIDTH, h: PADDLE_HEIGHT };

    const ball = { x: canvas.width / 2, y: canvas.height / 2, dx: 4, dy: 4 };

    let playerScore = 0;
    let aiScore = 0;

    // ─────────────────── Keyboard → "track‑pad" mapping ───────────────────
    const keyRows = [
      ["1", "2", "3", "4", "5", "6", "7", "8", "9", "0", "-", "="],
      ["q", "w", "e", "r", "t", "y", "u", "i", "o", "p", "[", "]", "\\"],
      ["a", "s", "d", "f", "g", "h", "j", "k", "l", ";", "'"],
      ["z", "x", "c", "v", "b", "n", "m", ",", ".", "/"],
    ];

    /** Map a pressed key to an (x,y) inside the bottom half of the canvas */
    function keyToPosition(key) {
      key = key.toLowerCase();
      let rowIdx = -1,
        colIdx = -1;
      for (let r = 0; r < keyRows.length; r++) {
        const c = keyRows[r].indexOf(key);
        if (c !== -1) {
          rowIdx = r;
          colIdx = c;
          break;
        }
      }
      if (rowIdx === -1) return null;
      const row = keyRows[rowIdx];
      const halfH = canvas.height / 2;
      const rowH = halfH / keyRows.length;
      const y = halfH + rowH * (rowIdx + 0.5);
      const x = ((colIdx + 0.5) / row.length) * canvas.width;
      return { x, y };
    }

    function handleKey(e) {
      const pos = keyToPosition(e.key);
      if (!pos) return;
      // Start animation toward new position
      player.startX = player.x;
      player.startY = player.y;
      player.targetX = pos.x;
      player.targetY = pos.y;
      player.moveStart = performance.now();
    }

    window.addEventListener("keydown", handleKey);

    // ─────────────────── Core loop ───────────────────
    function loop(timestamp) {
      ctx.clearRect(0, 0, canvas.width, canvas.height);

      // ─── Update: Ball ───
      ball.x += ball.dx;
      ball.y += ball.dy;

      // Left/right walls
      if (ball.x - BALL_RADIUS < 0 || ball.x + BALL_RADIUS > canvas.width) {
        ball.dx *= -1;
      }

      // Scoring (top/bottom)
      if (ball.y - BALL_RADIUS < 0) {
        playerScore++;
        resetBall(4);
      } else if (ball.y + BALL_RADIUS > canvas.height) {
        aiScore++;
        resetBall(-4);
      }

      // Paddle collisions with speed boost
      collidePaddle(player);
      collidePaddle(ai);

      // ─── Update: AI paddle ───
      const targetX = ball.x;
      const diff = targetX - ai.x;
      const aiMax = 5;
      ai.x += Math.max(-aiMax, Math.min(aiMax, diff));

      // ─── Update: Player paddle animation ───
      if (player.targetX !== null) {
        const elapsed = timestamp - player.moveStart;
        const t = Math.min(1, elapsed / PLAYER_MOVE_DURATION);
        player.x = player.startX + (player.targetX - player.startX) * t;
        player.y = player.startY + (player.targetY - player.startY) * t;
        if (t === 1) {
          player.targetX = player.targetY = null; // Done
        }
      }

      // ─── Render ───
      drawMidline();
      drawPaddle(player, "#10b981"); // green
      drawPaddle(ai, "#3b82f6"); // blue
      drawBall();
      drawHUD();

      requestAnimationFrame(loop);
    }

    // ─────────────────── Helpers ───────────────────
    function resetBall(initialDY) {
      ball.x = canvas.width / 2;
      ball.y = canvas.height / 2;
      ball.dx = Math.random() > 0.5 ? 4 : -4;
      ball.dy = initialDY;
    }

    function collidePaddle(p) {
      if (
        ball.x + BALL_RADIUS > p.x - p.w / 2 &&
        ball.x - BALL_RADIUS < p.x + p.w / 2 &&
        ball.y + BALL_RADIUS > p.y - p.h / 2 &&
        ball.y - BALL_RADIUS < p.y + p.h / 2 &&
        (p === player ? ball.dy > 0 : ball.dy < 0)
      ) {
        // Reverse vertical direction
        ball.dy *= -1;
        // Slight horizontal control based on hit position
        const offset = (ball.x - p.x) / (p.w / 2);
        ball.dx += offset * 5;
        // Accelerate!
        ball.dx *= SPEED_MULTIPLIER;
        ball.dy *= SPEED_MULTIPLIER;
      }
    }

    function drawPaddle(p, color) {
      ctx.fillStyle = color;
      ctx.fillRect(p.x - p.w / 2, p.y - p.h / 2, p.w, p.h);
    }

    function drawBall() {
      ctx.fillStyle = "#ef4444"; // red
      ctx.beginPath();
      ctx.arc(ball.x, ball.y, BALL_RADIUS, 0, Math.PI * 2);
      ctx.fill();
    }

    function drawMidline() {
      ctx.fillStyle = "#9ca3af";
      ctx.fillRect(0, canvas.height / 2 - 1, canvas.width, 2);
    }

    function drawHUD() {
      ctx.font = "20px monospace";
      ctx.fillStyle = "#111827";
      ctx.fillText(`${playerScore}`, 20, canvas.height / 2 + 30);
      ctx.fillText(`${aiScore}`, 20, 30);
    }

    // Start game!
    requestAnimationFrame(loop);

    // Cleanup
    return () => {
      window.removeEventListener("keydown", handleKey);
      window.removeEventListener("resize", resize);
    };
  }, []);

  return (
    <div className="flex flex-col items-center justify-center w-full h-full gap-4 p-4">
      <h1 className="text-4xl font-bold tracking-tight">Keyboard Pong</h1>
      <canvas ref={canvasRef} className="border-2 border-gray-400 rounded-2xl shadow-lg" />
      <p className="text-center text-gray-600 max-w-prose">
        Slide your finger across the keyboard rows (<kbd>1 … =</kbd>, <kbd>QWERTY</kbd>, <kbd>ASDF</kbd>, <kbd>ZXCV</kbd>) to move your
        paddle around.
      </p>
    </div>
  );
}
