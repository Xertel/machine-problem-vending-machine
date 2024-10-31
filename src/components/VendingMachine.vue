<script setup>
import PaymentInterface from './PaymentInterface.vue'
import ShopInterface from './ShopInterface.vue'

</script>

<script>
export default {
  data() {
    return {
      vmData: {
        totalOwed: 0,
        totalMoney: 1000,
        denominations: [1000, 500, 200, 100, 50, 20, 10, 5, 1]
      }
    }
  }
}
</script>

<template>
  <div class="main">
    <ShopInterface v-model:totalOwed="vmData.totalOwed" />
    <PaymentInterface v-model:vmData="vmData"/>
  </div>
</template>

<style scoped>
.main {
  color: black;
  --padding: 2em;
  margin: var(--padding);
  width: calc(100dvw - var(--padding)*2);
  height: calc(100dvh - var(--padding)*2);
  display: flex;
  gap: var(--padding);
  overflow: hidden;
  position: absolute;
}

@media only screen and (max-width: 768px) {
  .main {
    --padding: 1em;
    height: auto;
    flex-direction: column;
    overflow: auto;
    padding-bottom: 2em;
  }
}
</style>
