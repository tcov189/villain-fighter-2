<template>
  <div class="modal fade" id="special-modal">
    <div class="modal-dialog">
      <div class="modal-content">
        <img :src="imgSrc" alt />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: [
    'imgSrc',
  ],
};
</script>

<style>
</style>
