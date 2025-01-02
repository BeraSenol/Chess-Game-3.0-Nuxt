<template>
	<div class="max-w-screen">
		<div v-for="ranks, rank in chess.board()" class="flex">
			<div v-for="tile, file in ranks" :key="tile?.square" :id="getId(file, rank)" class="u-tile-size relative"
				:class="(file + rank) % 2 === 0 ? 'u-tile-light' : 'u-tile-dark'">
				<!-- <p class="text-black absolute">{{ getId(file, rank) }}</p> -->
				<NuxtImg v-if="tile" class="u-tile-size" :src="`/pieces/${tile.type}${tile.color}.svg`"
					:alt="`${tile.type}${tile.color}.svg`" :id="`${getId(file, rank)}-piece`"
					@click="hightlightMoves(<Square>getId(file, rank))" />
				<Indicator :id="`${getId(file, rank)}-indicator`" />
			</div>
		</div>
	</div>
</template>

<script lang="ts" setup>
import { Chess, type Square } from 'chess.js'

const chess = new Chess();

const getId = (fileIndex: number, rankIndex: number): string => {
	let fileLabel: string = '';
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

const hightlightMoves = (tile: Square) => {
	for (let i = 0; i < chess.moves({ square: tile }).length; i++) {
		document.getElementById(`${chess.moves({ square: tile, verbose: true })[i].to}-indicator`)?.classList.add('highlighted')
	}
}
</script>
