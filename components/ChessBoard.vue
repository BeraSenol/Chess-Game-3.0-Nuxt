<template>
  <UContainer>
    <div v-for="ranks, rank in chess.board()" class="flex">
      <div v-for="tile, file in ranks" :key="tile?.square" :id="generateId(file, rank)" class="u-tile-size"
        :class="(file + rank) % 2 === 0 ? 'u-tile-light' : 'u-tile-dark'">
        <p class="text-black absolute">{{ generateId(file, rank) }}</p>
        <div class="u-tile-size absolute chess-tile highlighted"></div>
        <NuxtImg v-if="tile" class="u-tile-size" :src="`/pieces/${tile.type}${tile.color}.svg`"
          :alt="`${tile.type}${tile.color}.svg`" @click="hightlightMoves(tile.square)" />
      </div>
    </div>
  </UContainer>
</template>

<script lang="ts" setup>
import type { _square } from '#tailwind-config/theme/aspectRatio';
import { Chess, type Square } from 'chess.js'

const chess = new Chess();

const generateId = (file: number, rank: number): string => {
  let id = '';
  switch (file) {
    case 0: id = 'a';
      break;
    case 1: id = 'b';
      break;
    case 2: id = 'c';
      break;
    case 3: id = 'd';
      break;
    case 4: id = 'e';
      break;
    case 5: id = 'f';
      break;
    case 6: id = 'g';
      break;
    case 7: id = 'h';
      break;
  }

  switch (rank) {
    case 0: id += '8';
      break;
    case 1: id += '7';
      break;
    case 2: id += '6';
      break;
    case 3: id += '5';
      break;
    case 4: id += '4';
      break;
    case 5: id += '3';
      break;
    case 6: id += '2';
      break;
    case 7: id += '1';
      break;
  }
  return `${id}`;
}

const hightlightMoves = (target: Square) => {
  for (let i = 0; i < chess.moves({ square: target }).length; i++) {
    const square = document.getElementById(chess.moves({ square: target })[i]);
    square?.classList.add('bg-black');
  }
}
</script>

<style scoped>
/* .chess-tile {
  display: flex;
  align-items: center;
  justify-content: center;
} */

.chess-tile.highlighted::before {
  content: '';
  width: 30px;
  /* Adjust size */
  height: 30px;
  /* Adjust size */
  background-color: rgba(0, 0, 0, 0.20);
  border-radius: 50%;
  pointer-events: none;
  /* Prevent interference with clicks */
}
</style>
