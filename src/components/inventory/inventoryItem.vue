<template>
  <div class="inventory-item__draggable">
    <div class="inventory-item__img">
      <img :src=item.image alt="">
    </div>
    <div class="inventory-item__count">
      <span> {{item.count}} </span>
    </div>
  </div>

</template>

<script>
import {ref} from "vue";
export default {
  name: "inventoryItem",
  props: ['item'],
  setup(){
  }
}
</script>

<style lang="scss">
@import "src/scss/inventory/inventoryItem.scss";
</style>