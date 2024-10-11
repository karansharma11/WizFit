<template>
  <div class="banner">
    <img src="../assets/banner.png" alt="Banner image" />
  </div>
</template>

<style scoped>
.banner {
  width: 100%;
  margin: 0 auto;
  display: flex;
  justify-content: center;
}

.banner img {
  width: 100%;
  height: auto;
}

/* Media Queries for responsiveness */
@media (max-width: 768px) {
  .banner img {
    border-radius: 8px;
  }
}

@media (max-width: 480px) {
  .banner img {
    border-radius: 5px;
  }
}
</style>
