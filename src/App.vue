<template>
  <div class="page">
    <div class="glow glow-left" />
    <div class="glow glow-right" />

    <div class="poster">
      <div class="logo-wrap">
        <div class="logo-badge">
          <div class="logo-text-group">
            <span class="logo-epic">EPIC</span>
            <span class="logo-millions">MILLIONS</span>
          </div>
          <div class="logo-ball">25</div>
        </div>
      </div>

      <h1 class="results-heading">Results for {{ draw.date }}</h1>

      <div class="prizes-row">
        <div v-for="(tier, i) in draw.tiers" :key="i" class="tier-col">
          <div class="balls-group">
            <div
              v-for="(ball, j) in tier.balls"
              :key="j"
              class="ball"
              :style="{
                background: ball.bg,
                boxShadow: `0 8px 28px ${ball.glow}`,
                animationDelay: `${ball.delay}s`
              }"
            >
              {{ ball.n }}
            </div>
          </div>
          <p class="tier-name">{{ tier.name }}</p>
          <p class="tier-points">{{ tier.points }}</p>
          <p class="tier-winners">{{ tier.winners }}</p>
        </div>
      </div>

      <p class="next-draw">Next Draw: {{ draw.nextDraw }}</p>
    </div>
  </div>
</template>

<script setup>
let globalIndex = 0

function makeBall(n, bg, glow) {
  return { n, bg, glow, delay: (globalIndex++ * 0.35) + 0.2 }
}

const draw = {
  date: 'Thursday, April 23, 2026',
  nextDraw: 'Sunday, May 3, 2026',
  tiers: [
    {
      name: 'Jackpot Prize',
      points: '13,000,000 Epic Points',
      winners: '0 winners',
      balls: [
        makeBall(22, 'radial-gradient(circle at 35% 30%, #60a5fa, #2563eb, #1e3a8a)', 'rgba(37,99,235,0.65)')
      ]
    },
    {
      name: '2nd Prize',
      points: '200,000 Epic Points',
      winners: '1 winner',
      balls: [
        makeBall(8,  'radial-gradient(circle at 35% 30%, #f87171, #dc2626, #991b1b)', 'rgba(220,38,38,0.65)'),
        makeBall(13, 'radial-gradient(circle at 35% 30%, #4ade80, #16a34a, #14532d)', 'rgba(22,163,74,0.65)')
      ]
    },
    {
      name: '3rd Prize',
      points: '3,000 Epic Points',
      winners: '55 winners',
      balls: [
        makeBall(11, 'radial-gradient(circle at 35% 30%, #4ade80, #16a34a, #14532d)', 'rgba(22,163,74,0.65)'),
        makeBall(31, 'radial-gradient(circle at 35% 30%, #fde047, #d97706, #92400e)', 'rgba(217,119,6,0.65)')
      ]
    },
    {
      name: '4th Prize',
      points: '1,000 Epic Points',
      winners: '866 winners',
      balls: [
        makeBall(18, 'radial-gradient(circle at 35% 30%, #4ade80, #16a34a, #14532d)', 'rgba(22,163,74,0.65)')
      ]
    }
  ]
}
</script>

<style>
*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Inter', sans-serif;
  background: #080b1a;
  min-height: 100dvh;
  overflow-x: hidden;
}

.page {
  position: relative;
  min-height: 100dvh;
  display: flex;
  align-items: center;
  justify-content: center;
  background:
    radial-gradient(ellipse 60% 50% at 15% 40%, rgba(60, 20, 120, 0.55) 0%, transparent 70%),
    radial-gradient(ellipse 55% 45% at 85% 60%, rgba(10, 30, 90, 0.5) 0%, transparent 70%),
    #090b1c;
  padding: 3rem 2rem;
}

.glow {
  position: fixed;
  border-radius: 50%;
  filter: blur(100px);
  pointer-events: none;
}

.glow-left {
  width: 600px;
  height: 600px;
  background: radial-gradient(circle, rgba(90, 30, 180, 0.4), transparent 70%);
  top: -150px;
  left: -200px;
}

.glow-right {
  width: 500px;
  height: 500px;
  background: radial-gradient(circle, rgba(20, 50, 140, 0.4), transparent 70%);
  bottom: -120px;
  right: -150px;
}

.poster {
  position: relative;
  width: 100%;
  max-width: 1100px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2.5rem;
}

.logo-wrap {
  display: flex;
  justify-content: center;
}

.logo-badge {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  background: linear-gradient(160deg, #5c1a0a, #2d0c04);
  border: 3px solid #c8860a;
  border-radius: 12px 12px 50% 50% / 12px 12px 30px 30px;
  padding: 0.9rem 2.4rem 1.6rem;
  min-width: 180px;
  box-shadow:
    0 0 0 1px rgba(200, 134, 10, 0.3) inset,
    0 8px 32px rgba(0, 0, 0, 0.6);
}

.logo-badge::before {
  content: '';
  position: absolute;
  inset: 4px;
  border-radius: 9px 9px 46% 46% / 9px 9px 26px 26px;
  border: 1px solid rgba(200, 134, 10, 0.2);
  pointer-events: none;
}

.logo-text-group {
  display: flex;
  flex-direction: column;
  align-items: center;
  line-height: 1;
}

.logo-epic {
  font-family: 'Rajdhani', sans-serif;
  font-size: 2.4rem;
  font-weight: 700;
  letter-spacing: 0.08em;
  background: linear-gradient(180deg, #fde68a, #d97706);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.logo-millions {
  font-family: 'Rajdhani', sans-serif;
  font-size: 1.5rem;
  font-weight: 700;
  letter-spacing: 0.12em;
  color: #ffffff;
}

.logo-ball {
  position: absolute;
  bottom: -20px;
  width: 42px;
  height: 42px;
  border-radius: 50%;
  background: radial-gradient(circle at 35% 30%, #60a5fa, #1d4ed8, #1e3a8a);
  box-shadow: 0 4px 16px rgba(29, 78, 216, 0.7);
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: 'Rajdhani', sans-serif;
  font-size: 1rem;
  font-weight: 700;
  color: #fff;
  border: 2px solid rgba(255, 255, 255, 0.25);
}

.results-heading {
  font-family: 'Rajdhani', sans-serif;
  font-size: clamp(1.6rem, 3.5vw, 2.6rem);
  font-weight: 700;
  color: #ffffff;
  letter-spacing: 0.02em;
  text-align: center;
  margin-top: 0.5rem;
}

.prizes-row {
  display: flex;
  align-items: flex-start;
  justify-content: center;
  gap: 1.5rem;
  width: 100%;
  flex-wrap: wrap;
}

.tier-col {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.9rem;
  flex: 1;
  min-width: 160px;
}

.balls-group {
  display: flex;
  gap: 0.6rem;
  justify-content: center;
  flex-wrap: wrap;
}

.ball {
  width: clamp(80px, 10vw, 120px);
  height: clamp(80px, 10vw, 120px);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: 'Rajdhani', sans-serif;
  font-size: clamp(1.8rem, 3.5vw, 3rem);
  font-weight: 700;
  color: #ffffff;
  user-select: none;
  flex-shrink: 0;
  opacity: 0;
  transform: translateY(-90px) scale(0.7);
  animation: dropBounce 0.75s cubic-bezier(0.22, 1, 0.36, 1) both;
}

@keyframes dropBounce {
  0% {
    opacity: 0;
    transform: translateY(-90px) scale(0.7);
  }
  50% {
    opacity: 1;
  }
  65% {
    transform: translateY(10px) scale(1.06);
  }
  80% {
    transform: translateY(-5px) scale(0.97);
  }
  90% {
    transform: translateY(3px) scale(1.01);
  }
  100% {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}
.tier-name {
  font-family: 'Rajdhani', sans-serif;
  font-size: clamp(1.1rem, 2vw, 1.45rem);
  font-weight: 700;
  color: #f59e0b;
  text-align: center;
  letter-spacing: 0.02em;
}

.tier-points {
  font-size: clamp(0.85rem, 1.4vw, 1rem);
  color: #e5e7eb;
  text-align: center;
  font-weight: 500;
}

.tier-winners {
  font-size: clamp(0.85rem, 1.4vw, 1rem);
  color: #e5e7eb;
  text-align: center;
  font-weight: 700;
}

.next-draw {
  font-family: 'Rajdhani', sans-serif;
  font-size: clamp(1.4rem, 3vw, 2.2rem);
  font-weight: 700;
  color: #ffffff;
  letter-spacing: 0.02em;
  text-align: center;
  padding-top: 0.5rem;
}
</style>
