<script setup>// logica
import VideoPlayer from './components/VideoPlayer.vue'
import VideoDetails from './components/VideoDetails.vue'
import VideoComments from './components/VideoComments.vue'
</script>

<template>
  <div class="app">
    <VideoPlayer class="playerBox" />
    <VideoDetails class="detailBox" />
    <VideoComments class="commentBox" />
  </div>
</template>

<style scoped>
.app {
  display: grid;
  display: grid;
grid-template-columns: 8fr 4fr;
grid-template-rows: 1fr 4fr;
grid-column-gap: 0px;
grid-row-gap: 0px;

overflow-y: hidden;
}

.playerBox { grid-area: 1 / 1 / 4 / 2; }
.detailBox { grid-area: 1 / 2 / 2 / 3; }
.commentBox { grid-area: 2 / 2 / 4 / 3; }

</style>
