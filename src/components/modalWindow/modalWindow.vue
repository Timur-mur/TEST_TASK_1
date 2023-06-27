<template>
  <div class="modal" v-bind:class="{ open: isActive }">
    <div class="modal__body">
      <div class="modal__content">
        <close-button @click="isActive=false"/>
        <div class="modal__img">
          <img :src=item alt="">
        </div>
        <div class="modal__title">
          <div class="modal__title-box">
          </div>
        </div>
        <div class="modal__type" v-if="formType===1">
          <delete-button/>
        </div>
        <div class="modal__type" v-if="formType===2">
          <input-form/>
          <cancel-button/>
          <sumbit-button/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CloseButton from "@/components/UI/closeButton.vue";
import DeleteButton from "@/components/modalWindow/UI/deleteButton.vue";
import CancelButton from "@/components/modalWindow/UI/cancelButton.vue";
import SumbitButton from "@/components/modalWindow/UI/sumbitButton.vue";
import InputForm from "@/components/modalWindow/UI/inputForm.vue";

export default {
  name: "modalWindow",
  components: {InputForm, SumbitButton, CancelButton, DeleteButton, CloseButton},
  props: ['isActive', 'item'],
  data(){
    return{
      formType: 1
    }
  }
}
</script>

<style lang="scss">
@import "src/scss/modalWondow/inner_modal.scss";
</style>