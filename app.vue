<template>
  <main class="u-bg-100 xl:overflow-y-hidden xl:overscroll-none pb-0 xl:pb-14 duration-300">
    <Navigation :turn="chess.turn()" :in-check="chess.isCheck()" />
    <section class="flex flex-col xl:flex-row justify-around xl:mx-4 xl:space-x-4">
      <!-- BOARD FOR WHITE -->
      <div v-if="isBoardFlipped" class="flex justify-center select-none">
        <div class="flex flex-col flex-none">
          <div v-for="(rank, i) in chess.board()" class="flex rounded" :key="`${rank}-${i}`">
            <div v-for="(file, j) of rank" class="relative u-tile-size" :key="getSquare(i, j, true, false)"
              :class="chess.squareColor(getSquare(i, j, true, true)) === 'light' ? 'u-tile-light' : 'u-tile-dark'"
              :id="getSquare(i, j, true, false)" @click="onSquareClick(getSquare(i, j, true, true))">
              <ChessboardTileLabel :key="`${getSquare(i, j, true, false)}-label`" :square="getSquare(i, j, true, false)"
                :color="chess.squareColor(getSquare(i, j, true, true)) === 'light'" :player-white="true" />
              <ChessboardPiece v-if="file" :key="`${getSquare(i, j, true, false)}}-piece`"
                :type="chess.get(getSquare(i, j, true, true))?.type"
                :color="chess.get(getSquare(i, j, true, true))?.color" />
              <ChessboardIndicator :key="`${getSquare(i, j, true, true)}-indicator`"
                :id="`${getSquare(i, j, true, true)}-indicator`" />
            </div>
          </div>
        </div>
      </div>
      <!-- BOARD FOR BLACK -->
      <div v-if="!isBoardFlipped" class="flex justify-center select-none">
        <div class="flex flex-col flex-none">
          <div v-for="(rank, i) in chess.board().toReversed()" class="flex" :key="`${rank}-${i}`">
            <div v-for="(file, j) of rank.toReversed()" class="relative u-tile-size" :key="getSquare(i, j, true, false)"
              :class="chess.squareColor(getSquare(i, j, false, true)) === 'light' ? 'u-tile-light' : 'u-tile-dark'"
              :id="getSquare(i, j, false, false)" @click="onSquareClick(getSquare(i, j, false, true))">
              <ChessboardTileLabel :key="`${getSquare(i, j, true, false)}-label`"
                :square="getSquare(i, j, false, false)"
                :color="chess.squareColor(getSquare(i, j, false, true)) === 'light'" :player-white="false" />
              <ChessboardPiece v-if="file" :key="`${getSquare(i, j, false, false)}}-piece`"
                :type="chess.get(getSquare(i, j, false, true))?.type"
                :color="chess.get(getSquare(i, j, false, true))?.color" />
              <ChessboardIndicator :key="`${getSquare(i, j, true, true)}-indicator`"
                :id="`${getSquare(i, j, false, true)}-indicator`" />
            </div>
          </div>
        </div>
      </div>
      <Information class="mt-4 xl:mt-0" :san="san" :lan="lan" :fen="fen" :ascii="ascii" :captures-white="capturesWhite"
        :captures-black="capturesBlack" , :is-board-flipped="isBoardFlipped" />
    </section>
    <UModals :chess="chess" />
    <UNotifications />
  </main>
</template>

<script lang="ts" setup>
const { chess, san, lan, fen, ascii, capturesWhite, capturesBlack, isBoardFlipped, onSquareClick, getSquare } = useChess();
useHead({ htmlAttrs: { lang: 'en' } });
useSeoMeta({ title: 'Pretty Chess' });
</script>
