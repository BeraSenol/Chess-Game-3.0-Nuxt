<template>
  <div>
    <p v-if="square.charAt(0) === 'a'" :class="color ? 'text-primary-950' : 'text-white'" class="absolute left-0.5">
      {{ square.charAt(1) }} </p>
    <p v-if="square.charAt(1) === '1'" :class="color ? 'text-primary-950' : 'text-white'"
      class="absolute right-1 -bottom-0.5"> {{ square.charAt(0) }} </p>
  </div>
</template>

<script lang="ts">
export default {
  props: {
    square: { type: String, required: true },
    color: { type: Boolean, required: true }
  }
};
</script>