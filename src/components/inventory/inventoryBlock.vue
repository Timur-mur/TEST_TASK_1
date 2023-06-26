<template>
  <div class="inventory-block">
    <div v-for="category in categories"
         :key="category"
         @drop="onDrop($event, category)"
         class="inventory-block__droppable">
      <inventory-item
          v-for="item in items.filter(x => x.categoryId === category)"
          @dragstart="onDragStart($event, item)"
          v-bind:key="item.id"
          :item="item">
      </inventory-item>
    </div>
  </div>
</template>

<script lang="ts">
import ModalWindow from "@/components/modalWindow/modalWindow.vue";
import {ref} from "vue";
import InventoryItem from "@/components/inventory/inventoryItem.vue";

export default {
  name: "inventoryBlock",
  components: {InventoryItem, ModalWindow},
  setup(){
    const categories = ref([0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24])
    const items = ref([
      {
        id: 0,
        count: 4,
        image: require("../../assets/img/Item_green.svg"),
        categoryId: 0,
      },
      {
        id: 1,
        count: 2,
        image: require('../../assets/img/Item_orange.svg'),
        categoryId: 1,
      },
      {
        id: 2,
        count: 5,
        image: require("../../assets/img/Item_primary.svg"),
        categoryId: 2,
      },
    ])
    function onDrop(e: DragEvent, item) {
      e.dataTransfer.dropEffect = 'move'
      e.dataTransfer.effectAllowed = 'move'
      e.dataTransfer.setData('itemId', item.id.toString())
    }
    function onDragStart(e: DragEvent, category) {
      const itemId = parseInt(e.dataTransfer.getData('itemId'))
      items.value = items.value.map(x => {
        if(x.id === itemId)
          x.categoryId = category
        return x
      })
    }
    return {
      categories,
      items,
      onDrop,
      onDragStart
    }
  },
}
</script>

<style lang="scss">
@import "src/scss/inventory/inventoryBlock.scss";
</style>