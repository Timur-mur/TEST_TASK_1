<template>
  <div class="input__box">
    <close-button/>
    <input>
  </div>
</template>

<script>
import CloseButton from "@/components/UI/closeButton.vue";

export default {
  name: "inputForm",
  components: {CloseButton}
}
</script>

<style lang="scss">
@import "src/scss/sceletons/input.scss";
</style>