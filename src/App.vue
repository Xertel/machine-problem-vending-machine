<script setup>
import VendingMachine from './components/VendingMachine.vue'
</script>

<template>
  <main>
    <div>
      <VendingMachine />
    </div>
  </main>
</template>

<style scoped>
main {
  height: 100dvh;
  width: 100dvw;
  background-color: rgb(32, 32, 32);
  font-family: Poppins;
  --lighter-text: rgb(236, 236, 236);
  --light-text: rgb(228, 228, 228);
}

@media only screen and (max-width: 768px) {
  main {
    height: auto;
  }
}
</style>
