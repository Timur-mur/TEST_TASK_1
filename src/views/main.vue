<template>
  <div class="main-container">
    <card/>
    <inventory-block/>
    <input-form/>
  </div>
</template>

<script>
import Card from "@/components/sceletons/card.vue";
import InputForm from "@/components/sceletons/inputForm.vue";
import InventoryBlock from "@/components/inventory/inventoryBlock.vue";
import ModalWindow from "@/components/modalWindow/modalWindow.vue";

export default {
  name: "main",
  components: {ModalWindow, InventoryBlock, InputForm, Card }
}
</script>

<style lang="scss">
@import "src/scss/main.scss";
</style>