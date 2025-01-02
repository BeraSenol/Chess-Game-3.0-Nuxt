<template>
  <div class="u-tile-size  indicator"></div>
</template>

<script lang="ts" setup>

</script>

<style scoped>
div {
  display: flex;
  align-items: center;
  justify-content: center;
}

div .highlighted::after {
  position: absolute;
  content: '';

  background-color: rgba(0, 0, 0, 0.25);
  border-radius: 50%;
  pointer-events: none;
}
</style>