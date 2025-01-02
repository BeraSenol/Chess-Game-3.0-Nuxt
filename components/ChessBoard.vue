<template>
  <UContainer>
    <div v-for="ranks, rank in chess.board()" class="flex">
      <div v-for="tile, file in ranks" :key="tile?.square" :id="getId(file, rank)" class="u-tile-size relative"
        :class="(file + rank) % 2 === 0 ? 'u-tile-light' : 'u-tile-dark'">
        <p class="text-black absolute">{{ getId(file, rank) }}</p>
        <NuxtImg v-if="tile" class="u-tile-size" :src="`/pieces/${tile.type}${tile.color}.svg`"
          :alt="`${tile.type}${tile.color}.svg`" @click="hightlightMoves(tile.square)" />
        <Indicator :id="`${getId(file, rank)}-indicator`"/>
      </div>
    </div>
  </UContainer>
</template>

<script lang="ts" setup>
import type { _square } from '#tailwind-config/theme/aspectRatio';
import { Chess, type Square } from 'chess.js'

const chess = new Chess();

const getId = (fileIndex: number, rankIndex: number): string => {
  let fileLabel: string = '';
  console.log(chess.moves({square: 'b1'}))
  switch (fileIndex) {
    case 0: fileLabel = 'a';
      break;
    case 1: fileLabel = 'b';
      break;
    case 2: fileLabel = 'c';
      break;
    case 3: fileLabel = 'd';
      break;
    case 4: fileLabel = 'e';
      break;
    case 5: fileLabel = 'f';
      break;
    case 6: fileLabel = 'g';
      break;
    case 7: fileLabel = 'h';
      break;
  }
  return `${fileLabel}${8 - rankIndex}`;
}

const hightlightMoves = (target: Square) => {
  for (let i = 0; i < chess.moves({ square: target }).length; i++) {
    const indicator = document.getElementById(`${chess.moves({ square: target })[i]}-indicator`);
    indicator?.classList.add('highlighted');
  }
}
</script>
