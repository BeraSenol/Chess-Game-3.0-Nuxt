<template>
  <div class="grid grid-cols-8 grid-rows-8 gap-0 w-fit p-4">
    <div v-for="square, index in squares" :key="index" :id="square"
      :class="isLightSquare(index) ? 'bg-white' : 'bg-primary-900'" class="aspect-sqaure w-28 h-28">
      <p :class="isLightSquare(index) ? 'text-primary-900' : 'text-white'" class="ml-0.5">{{ square }}</p>
    </div>

  </div>
</template>

<script lang="ts" setup>
import { SQUARES } from 'chess.js'
import { Chess } from 'chess.js'

const squares = SQUARES;
const chess = new Chess();

const isLightSquare = (index: number) => {
  const file = index % 8; // Column
  const rank = Math.floor(index / 8); // Row
  return (file + rank) % 2 === 0;
};
</script>