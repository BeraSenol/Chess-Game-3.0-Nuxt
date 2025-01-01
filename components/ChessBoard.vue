<!-- <template>
  <div class="grid grid-cols-8 grid-rows-8 gap-0 w-fit p-4">
    <div v-for="square, index in squares" :key="index" :id="square"
      :class="isLightSquare(index) ? 'bg-white' : 'bg-primary-900'" class="aspect-sqaure w-28 h-28">
      <p :class="isLightSquare(index) ? 'text-primary-900' : 'text-white'" class="ml-0.5">{{ square }}</p>
    </div>
  </div>
</template> -->

<template>
  <div>
    <div v-for="ranks, rank in chess.board()" class="flex">
      <div v-for="tile, file in ranks" class="w-28 h-28"
        :class="isLightSquare(file, rank) ? 'bg-white' : 'bg-primary-900'">
        <NuxtImg v-if="tile" class="w-28 h-28" :src="getImagePath(tile.type, tile.color)"></NuxtImg>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { SQUARES } from 'chess.js'
import { Chess } from 'chess.js'

const squares = SQUARES;
const chess = new Chess();

const isLightSquare = (file: number, rank: number): boolean => {
  return (file + rank) % 2 === 0;
};

const getImagePath = (type: string, color: string): string => {
  return "pieces/" + type + color + ".svg";
}

</script>