<template>
  <div>
    <p v-if="file === 0" :class="color" class="absolute left-1">{{ label?.charAt(1) }}</p>
    <p v-if="rank === 7" :class="color" class="absolute right-1 bottom-0">{{ label?.charAt(0) }}</p>
  </div>
</template>

<script lang="ts">
export default {
  props: {
    file: { type: Number },
    rank: { type: Number },
    label: { type: String },
    color: {type: String}
  }
};
</script>