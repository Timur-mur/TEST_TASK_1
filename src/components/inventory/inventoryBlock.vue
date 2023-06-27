<template>
  <div class="inventory-block">
    <div v-for="category in categories"
         :key="category"
         @drop="onDrop($event, category)"
         @dragover.prevent
         @dragenter.prevent
         class="inventory-block__droppable">
      <inventory-item
          v-for="item in items.filter(x => x.categoryId === category)"
          @dragstart="onDragStart($event, item)"
          draggable="true"
          v-bind:key="item.id"
          :item="item"
          @click="clickItem(item)"
      >
      </inventory-item>
    </div>
    <modal-window :isActive="visible" :item="item"/>
  </div>
</template>

<script>
import ModalWindow from "@/components/modalWindow/modalWindow.vue";
import {ref} from "vue";
import InventoryItem from "@/components/inventory/inventoryItem.vue";

export default {
  name: "inventoryBlock",
  components: {InventoryItem, ModalWindow},
  data(){
    return{
      visible: false,
      item: '',
    }
  },
  setup(){
    let items = []
    if (localStorage.getItem("items")) {
      items = ref(JSON.parse(localStorage.getItem("items")))
    }
    else {
      items = ref([
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
      localStorage.setItem("items", JSON.stringify(items.value))
    }
    const categories = ref([0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24])
    function onDragStart(e, item) {
      e.dataTransfer.dropEffect = 'move'
      e.dataTransfer.effectAllowed = 'move'
      e.dataTransfer.setData('itemId', item.id.toString())
    }
    function onDrop(e, category) {
      const itemId = parseInt(e.dataTransfer.getData('itemId'))
      items.value = items.value.map(x => {
        if(x.id === itemId)
          x.categoryId = category
        return x
      })
      localStorage.setItem('items', JSON.stringify(items.value))
    }
    return {
      categories,
      items,
      onDrop,
      onDragStart,
    }
  },
  methods:{
    clickItem(item) {
      this.visible = !this.visible
      console.log(item.image.toString())
       this.item = item.image
    }
  }
}
</script>

<style lang="scss">
@import "src/scss/inventory/inventoryBlock.scss";
</style>