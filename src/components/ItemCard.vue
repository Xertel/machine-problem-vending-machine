<script setup>
  defineProps({
    name: {
      type: String, required: true
    },
    cost: {
      type: Number, required: true
    },
    img: {
      type: String, required: true
    }
  })
</script>

<template>
  <div class="item">
    <div class="picture-container">
      <img :src="img">
    </div>
    <div class="details-container">
      <div class="item-info">
        <div class="item-text" style="font-weight: bold;">
          {{ name }}
        </div>
        <div class="item-text">
          {{ "P " + cost }}
        </div>
      </div>
      <div class="buy-button-container">
        <button class="buy-button" @click="$emit('buy')">Buy</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.item {
  width: 100%;
  height: 428px;
  background-color: rgb(20, 20, 20);
  padding: 1.6em;
  display: flex;
  flex-direction: column;
  border-radius: 40px;
  box-shadow: 0px 0px 2px 1px rgb(82, 82, 82);
}

.picture-container {
  height: 100%;
  width: 100%;
  display: flex;
  justify-content: center;
}

img {
  height: 300px;
  width: 100%;
  border-radius: 20px;
  object-fit: cover;
}

.details-container {
  display: flex;
  justify-content: space-between;
  margin-top: 1.1em;
  margin-right: .2em;
  align-content: center;
}

.item-info {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.item-text {
  width: 100%; 
  font-size: 1.3em;
  color: var(--lighter-text);
}

.buy-button-container {
  display: flex;
  align-items: center;
}

.buy-button {
  color: var(--lighter-text);
  font-size: 1.2em;
  padding: 4px 12px;
  background-color: rgb(0, 64, 182);
  border-style: solid;
  border-width: 1px;
  border-color: rgb(0, 38, 109);
  border-radius: 8px;
}

</style>
