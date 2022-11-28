<template>
  <img
    class="Delivery-logo"
    alt="Delivery Logo"
    src="/delivery.gif"
  >
</template>

<style>
.Delivery-logo {
  padding: 100px;
  min-height: 600px;
  height: 800px;
  width: 100%;
  transform: rotateY(560deg);
  animation: turn 3.5s ease-out forwards 1s;
}

@keyframes turn {
  100% {
    transform: rotateY(0deg);
  }
}
</style>
