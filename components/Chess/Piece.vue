<template>
  <div>
    <NuxtImg class="u-tile-size" :src="`/pieces/${type}${color}.svg`" :alt="`${type}${color}.svg`" />
  </div>
</template>

<script lang="ts">
export default {
  props: {
    type: { type: String, required: true },
    color: { type: String, required: true },
  }
};
</script>
