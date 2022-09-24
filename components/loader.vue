<template>
  <svg class="spinner" viewBox="0 0 70 70">
    <circle
      class="circle"
      r="20"
      cx="35"
      cy="35"
      fill="none"
      stroke-width="7"
    />
  </svg>
</template>

<style lang="scss" scoped>
@keyframes dash {
  0% {
    stroke-dasharray: 1, 150;
    stroke-dashoffset: 0;
  }

  50% {
    stroke-dasharray: 90, 150;
    stroke-dashoffset: -35;
  }

  100% {
    stroke-dasharray: 100, 150;
    stroke-dashoffset: -124;
  }
}

@keyframes rotate {
  100% {
    transform: rotate(360deg);
  }
}

.spinner {
  position: absolute;
  top: 50%;
  left: 50%;
  margin: -35px 0 0 -35px;
  width: 70px;
  height: 70px;
  animation: rotate 2s linear infinite;
}

.circle {
  stroke: slategray;
  stroke-linecap: round;
  animation: dash 1.5s ease-in-out infinite;
}
</style>
