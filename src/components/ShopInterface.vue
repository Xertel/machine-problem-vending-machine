<script setup>
import ItemCard from './ItemCard.vue'
</script>

<script>
export default {
  props: {
    totalOwed: {
      type: Number,
      required: true
    }
  },
  emits: ['update:totalOwed'],
  computed: {
    totalOwedValue: {
      get() {
        return this.totalOwed
      },
      set(value) {
        this.$emit('update:totalOwed', value)
      }
    }
  },
  methods: {
    addTotalOwed(cost) {
      this.totalOwedValue += cost
    }
  },
}
</script>

<template>
  <div class="shop-container">
    <ItemCard name="Mountain Dew" :cost="64" @buy="addTotalOwed(64)" img="https://pbs.twimg.com/profile_images/1623072691291844608/4-AUWwuX_400x400.jpg" />
    <ItemCard name="Regular Coca Cola" :cost="42" @buy="addTotalOwed(42)" img="https://pbs.twimg.com/profile_images/1234873883850952704/JQhv0G7n_400x400.jpg" />
    <ItemCard name="Coca Cola Zero" :cost="41" @buy="addTotalOwed(41)" img="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRGso_IG9Jfj_fRaCAS257MK0e3JqQBGx1CjQ&s" />
    <ItemCard name="Pepsi" :cost="35" @buy="addTotalOwed(35)" img="https://i.pinimg.com/736x/a0/ea/30/a0ea30ee142bacf56cb730d0321192fe.jpg" />
    <ItemCard name="Sprite" :cost="21" @buy="addTotalOwed(21)" img="https://www.logotypes101.com/logos/520/5D7076E3BAAAE5E0FF3D7809FEB8E924/sprite_logo.png" />
    <ItemCard name="Royal" :cost="12" @buy="addTotalOwed(12)" img="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRIEj27yAvxvKBhjXl5IGjm5uGV_cvAtJw6Rg&s" />
    <ItemCard name="Jack Daniel's" :cost="243" @buy="addTotalOwed(243)" img="https://i.pinimg.com/236x/85/e5/c0/85e5c0f4838a9f22572bf75318cf1435.jpg" />
    <ItemCard name="Starbucks Coffee" :cost="172" @buy="addTotalOwed(172)" img="https://cdn.logoworks.com/wp-content/uploads/2017/06/Untitled-2-640x360-1.png" />
    <ItemCard name="Mug Root Beer" :cost="72" @buy="addTotalOwed(72)" img="https://i.redd.it/i-turned-my-friends-dog-into-the-mug-root-beer-logo-v0-rci01oky5z7a1.jpg?width=720&format=pjpg&auto=webp&s=fd3c37172a43a254ee8c49a9145d14bd266a7d6c" />
  </div>
</template>

<style scoped>
.shop-container {
  flex-grow: 7;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  align-content: start;
  gap: 2em;
  height: 100%;
  width: 100%;
  padding: 0em 4em;
  overflow-y: auto;
  position: relative;
  -ms-overflow-style: none;
  scrollbar-width: none;
}

.shop-container > div {
  flex-basis: 320px;
  flex-grow: 1;
}

.shop-container::-webkit-scrollbar {
    display: none;
}

@media only screen and (max-width: 768px) {
  .shop-container {
    height: auto;
    width: 100%;
    flex-direction: row;
    overflow: auto;
    padding: 4em 0em;
  }
}
</style>
