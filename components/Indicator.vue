<template>
  <div class="u-tile-size absolute indicator"></div>
</template>

<script lang="ts" setup>

</script>

<style scoped>
.indicator {
  display: flex;
  align-items: center;
  justify-content: center;
}

.indicator.highlighted::before {
  content: '';
  width: 30px;
  height: 30px;
  background-color: rgba(0, 0, 0, 0.20);
  border-radius: 50%;
  pointer-events: none;
}
</style>