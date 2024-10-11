<template>
  <Banner />
  <div class="below-banner">
    <div class="title">What is WizFit challenge?</div>
    <div>
      <button class="watch-video">
        <i class="fa-solid fa-caret-right watch-icon"></i>Watch Video
      </button>
    </div>
  </div>
  <div class="player">
    <img src="./assets/player.png" alt="Player image" />
  </div>
  <SearchCard />
</template>

<script setup>
import Banner from './components/Banner.vue'
import SearchCard from './components/SearchCard.vue'
</script>

<style scoped>
.below-banner {
  max-width: 100%;
  margin: 20px auto;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  text-align: center;
  gap: 15px;
}

.title {
  font-size: 40px;
  font-weight: 800;
  text-align: center;
  margin-bottom: 10px;
  margin-top: 5px;
}

.watch-video {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 10px 20px;
  background-color: rgb(207, 30, 104);
  color: white;
  font-size: 16px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.watch-icon {
  font-size: 28px;
  margin-right: 10px;
}

.watch-video:hover {
  background-color: rgb(185, 25, 92);
}

.player {
  max-width: 500px;
  margin: 20px auto 0 auto;
  text-align: center;
}

.player img {
  width: 100%;
  height: auto;
  border-radius: 10px;
}

/* Media Queries for responsiveness */
@media (max-width: 768px) {
  .below-banner {
    max-width: 100%;
    margin: 20px auto;
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    gap: 10px;
  }

  .title {
    font-size: 22px;
  }

  .watch-icon {
    font-size: 24px;
  }

  .watch-video {
    padding: 8px 16px;
    font-size: 14px;
  }

  .player {
    max-width: 350px;
  }
}

@media (max-width: 480px) {
  .title {
    font-size: 20px;
  }

  .watch-icon {
    font-size: 20px;
  }

  .watch-video {
    padding: 6px 12px;
    font-size: 12px;
  }

  .player {
    max-width: 100%;
  }
}
</style>
