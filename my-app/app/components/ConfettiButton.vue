<!-- ConfettiButton.vue -->
<template>
    <div class="container">
      <button @click="createConfetti" class="button">
        🎉 Pop the Confetti! 🎉
      </button>
      
      <div
        v-for="piece in confetti"
        :key="piece.id"
        class="confetti-piece"
        :style="{
          left: `${piece.left}px`,
          top: `${piece.top}px`,
          width: piece.shape === 'rectangle' ? `${piece.size * 2}px` : `${piece.size}px`,
          height: `${piece.size}px`,
          backgroundColor: piece.color,
          borderRadius: piece.shape === 'circle' ? '50%' : '0',
          animation: `confettiExplode ${piece.duration}s cubic-bezier(0.25, 0.46, 0.45, 0.94) forwards`,
          '--velocity-x': `${piece.velocityX}px`,
          '--velocity-y': `${piece.velocityY}px`
        }"
      />
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const confetti = ref([]);
  
  const createConfetti = (e) => {
    const rect = e.currentTarget.getBoundingClientRect();
    const buttonCenterX = rect.left + rect.width / 2;
    const buttonCenterY = rect.top + rect.height / 2;
    
    const newConfetti = [];
    const colors = ['#ff0000', '#00ff00', '#0000ff', '#ffff00', '#ff00ff', '#00ffff', '#ffa500', '#ff69b4', '#fff', '#ffd700'];
    const shapes = ['square', 'circle', 'rectangle'];
    
    for (let i = 0; i < 150; i++) {
      const angle = (Math.PI * 2 * i) / 150;
      const velocity = 3 + Math.random() * 4;
      const velocityX = Math.cos(angle) * velocity * 100;
      const velocityY = Math.sin(angle) * velocity * 100;
      
      newConfetti.push({
        id: Date.now() + Math.random() + i,
        left: buttonCenterX,
        top: buttonCenterY,
        color: colors[Math.floor(Math.random() * colors.length)],
        velocityX,
        velocityY,
        size: Math.random() * 8 + 4,
        shape: shapes[Math.floor(Math.random() * shapes.length)],
        duration: 2 + Math.random()
      });
    }
    
    confetti.value = newConfetti;
    
    setTimeout(() => {
      confetti.value = [];
    }, 3500);
  };
  </script>
  
  <style scoped>
  .container {
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    background: linear-gradient(135deg, #a855f7 0%, #ec4899 50%, #ef4444 100%);
    overflow: hidden;
    position: relative;
  }
  
  .button {
    position: relative;
    z-index: 10;
    padding: 20px 40px;
    font-size: 28px;
    font-weight: bold;
    color: white;
    background: linear-gradient(135deg, #3b82f6, #9333ea);
    border: 4px solid white;
    border-radius: 50px;
    cursor: pointer;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
    transition: all 0.2s;
  }
  
  .button:hover {
    transform: scale(1.05);
    box-shadow: 0 15px 40px rgba(0, 0, 0, 0.4);
  }
  
  .button:active {
    transform: scale(0.95);
  }
  
  .confetti-piece {
    position: fixed;
    pointer-events: none;
    z-index: 20;
  }
  
  @keyframes confettiExplode {
    0% {
      transform: translate(0, 0) rotate(0deg) scale(1);
      opacity: 1;
    }
    10% {
      opacity: 1;
    }
    100% {
      transform: translate(var(--velocity-x), calc(var(--velocity-y) + 800px)) rotate(720deg) scale(0.5);
      opacity: 0;
    }
  }
  </style>