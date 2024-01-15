<template>
  <div id="app">
    <animation-screen v-if ="page === 0" @next-page = "page++"></animation-screen>
    <open-screen v-else-if ="page === 1" @next-page = nextPage></open-screen>
    <asteroid-type v-else-if ="page === 2" @prev-page = prevPage @start-game = nextPage></asteroid-type>
    <game-screen v-else-if ="page === 3"></game-screen>
  </div>
</template>
 
<script>
import AnimationScreen from '@/components/AnimationScreen.vue';
import OpenScreen from '@/components/OpenScreen.vue';
import AsteroidType from '@/components/AsteroidType.vue';
import GameScreen from '@/components/GameScreen.vue';

export default {

  name: "app",
  components: {
    OpenScreen,
    AsteroidType,
    GameScreen,
    AnimationScreen
  },
  data() {
    return {
      page: 0,
    };
  },
  methods: {
    nextPage() {
      this.page++;
    },
    prevPage() {
      this.page--;
    }, 
  },
};
</script>

<style>
@font-face {
  font-family: 'Heebo';
  src: url('@/assets/heebo.regular.ttf');
}
@font-face {
  font-family: 'Heebo-Bold';
  src: url('@/assets/heebo.black.ttf');
}
* {
  overflow: hidden;
  font-family: 'Heebo';
}
body {
  width: 100%;
	height: 100%;
	direction: rtl;
  overflow: hidden;
	margin: 0%;
}

#app {
  font-family: 'Heebo';
}


</style>