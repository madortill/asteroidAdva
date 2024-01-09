<template>
  <div id="animation-screen">
    <div class="main-title">
      <img class="Spaceship" src="@/assets/till.svg" />
      <h1 class="title">ברוכים הבאים ללומדת האסטרואיד</h1>
      <button v-if="!showAnimation" class="btnStart" @click="startAnimation"> התחל לומדה</button>
      <div class="canvas">
        <div class="earth">
          <div class="land-big na">
            <div class="land l-1"></div>
            <div class="land-join"></div>
            <div class="land l-2"></div>
          </div>
          <div class="land-big sa">
            <div class="land l-1"></div>
            <div class="land-join"></div>
            <div class="land l-2"></div>
          </div>
          <div class="land-big ce">
            <div class="land l-1"></div>
            <div class="land-join"></div>
            <div class="land-join j-2"></div>
            <div class="land l-2"></div>
            <div class="land l-3"></div>
          </div>
          <div class="land-big a">
            <div class="land l-1"></div>
            <div class="land-join"></div>
            <div class="land l-2"></div>
          </div>
          <div class="land ne"></div>
          <div class="land au"></div>
          <div class="land np"></div>
          <div class="land sp"></div>
          <div class="cloud-wrapper">
            <div class="cloud c1"></div>
            <div class="cloud c2"></div>
            <div class="cloud c3"></div>
            <div class="cloud c4"></div>
            <div class="cloud c5"></div>
            <div class="cloud c6"></div>
            <div class="cloud c7"></div>
            <div class="cloud c8"></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "animation-screen",
  data() {
    return {
      showAnimation: false,
    };
  },
  methods: {
    startAnimation() {
      // this.showAnimation = true;
      this.$emit('next-page');
    },
  },
};
</script>

<style>
#animation-screen {
  height: 100vh;
  width: 100vw;
}

:root {
  --space-color: #0f2437;
  --earth-water-color: #2276bc;
  --earth-land-color: #65c547;
  --earth-cloud-color: #e6e8d2;
  --earth-rotation: 20000ms;
  --cloud-rotation: 30000ms;
}

body {
  background-image: url("@/assets/Blue Gradient Flat Space Planet Advertising Background Wallpaper Image For Free Download - Pngtree.jpg");
  background-repeat: no-repeat;
  background-size: cover;
}

.main-title {
  color: #e6e8d2;
  text-align: center;
  margin-top: 25%;
  height: 100vh;
  width: 100vw;
}

.btnStart {
  background-color: #61a5c2;
  border-radius: 5vw;
  bottom: 9vh;
  position: relative;
  outline: 2px solid #61a5c2;
  width: 25%;
  height: 6vh;
  font-family: 'Heebo-bold';
  color: #e6e8d2;
  cursor: pointer;
}

.title {
  animation: floatAnimation 2s ease-in-out infinite;
  font-family: 'Heebo-Bold';
  padding: 5%;
  position: relative;
  bottom: 9vh;
  max-width: 70%;
  min-width: 90%;
}

.Spaceship {
  width: 30%;
  position: relative;
  top: 70vh;
  left: 40vw;
  /* animation: SpaceshipAnimation 4s linear forwards,rotateToLeft 4s 4.5s linear ; */
  animation: all 6s linear forwards;
}

.canvas {
  position: relative;
  display: block;
  margin: auto;
  margin-top: 5%;
  width: 100%;
  height: 100%;
  border-radius: 5px;
  background: none;
}


/* Earth */

.earth {
  position: relative;
  width: 200px;
  height: 200px;
  border-radius: 50%;
  background-color: var(--earth-water-color);
  right: 38vw;
  overflow: hidden;
  -webkit-transform: translate3d(0, 0, 0);
  -moz-transform: translate3d(0, 0, 0);
  transform: rotate(15deg);
  z-index: 10;
}

.earth:after {
  content: '';
  position: absolute;
  height: 200px;
  width: 200px;
  border-radius: 50%;
  box-shadow: inset -50px -25px rgba(0, 0, 0, 0.2);
}

.land {
  position: absolute;
  background-color: var(--earth-land-color);
  border-radius: 20px;
}

.land-big {
  position: absolute;
  background-color: var(--earth-land-color);
  border-radius: 16px;
}

.land-join {
  position: absolute;
  background-color: var(--earth-land-color);
  height: 10px;
  width: 30px;
}

.cloud {
  position: absolute;
  background-color: var(--earth-cloud-color);
  border-radius: 20px;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.10);
}

.land-join::before {
  content: '';
  position: absolute;
  left: -5px;
  height: 10px;
  width: 10px;
  border-radius: 50%;
  background: var(--earth-water-color);
  box-shadow: 30px 0px 0px var(--earth-water-color);
}

/* Animate the land */



@keyframes all {
  0% {
    transform: translateY(10vh);
  }

  30% {
    transform: translateY(-70vh);
  }

  50% {
    transform: translateY(-70vh) rotate(-120deg);
  }

  70% {
    transform: translate(-60vw, -35vh) rotate(-50deg)
  }

  100% {
    transform: translate(-55vw, -30vh)
  }
}

@keyframes earth-rotation-a-start {
  0% {
    transform: translate(0px);
  }

  100% {
    transform: translate(250px);
  }
}

@keyframes earth-rotation-a-loop {
  0% {
    transform: translate(-200px);
  }

  100% {
    transform: translate(250px);
  }
}

@keyframes earth-rotation-ce-start {
  0% {
    transform: translate(0px);
  }

  100% {
    transform: translate(150px);
  }
}

@keyframes earth-rotation-ce-loop {
  0% {
    transform: translate(-350px);
  }

  100% {
    transform: translate(100px);
  }
}

/* Animate the cloud */

@keyframes earth-rotation-cla-start {
  0% {
    transform: translate(0px);
  }

  100% {
    transform: translate(250px);
  }
}

@keyframes earth-rotation-cla-loop {
  0% {
    transform: translate(-150px);
  }

  100% {
    transform: translate(250px);
  }
}

@keyframes earth-rotation-cle-start {
  0% {
    transform: translate(0px);
  }

  100% {
    transform: translate(100px);
  }
}

@keyframes earth-rotation-cle-loop {
  0% {
    transform: translate(-200px);
  }

  100% {
    transform: translate(150px);
  }
}

@keyframes floatAnimation {
  0% {
    transform: translateY(0);
  }

  50% {
    transform: translateY(-10px);
  }

  100% {
    transform: translateY(0);
  }
}

/*  Big land NA */

.land-big.na {
  top: 30px;
  left: -30px;
  animation-name: earth-rotation-a-start, earth-rotation-a-loop;
  animation-duration: 13000ms, var(--earth-rotation);
  animation-timing-function: linear;
  animation-delay: 0s, 13000ms;
  animation-iteration-count: 1, infinite;
}

.land-big.na>.land-join {
  top: 25px;
  left: 37px;
}

.na>.l-1 {
  left: -30px;
  height: 25px;
  width: 130px;
}

.na>.l-2 {
  top: 35px;
  height: 35px;
  width: 80px;
}

/* Big land SA */

.land-big.sa {
  top: 120px;
  animation-name: earth-rotation-a-start, earth-rotation-a-loop;
  animation-duration: 13000ms, var(--earth-rotation);
  animation-timing-function: linear;
  animation-delay: 0s, 13000ms;
  animation-iteration-count: 1, infinite;
}

.land-big.sa>.land-join {
  top: 25px;
  left: 20px;
}

.sa>.l-1 {
  height: 25px;
  width: 80px;
}

.sa>.l-2 {
  top: 35px;
  height: 20px;
  width: 110px;
}

/* Big land A */

.land-big.a {
  top: 100px;
  left: 109px;
  animation-name: earth-rotation-ce-start, earth-rotation-ce-loop;
  animation-duration: 8000ms, var(--earth-rotation);
  animation-timing-function: linear;
  animation-delay: 0s, 5200ms;
  animation-iteration-count: 1, infinite;
}

.land-big.a>.land-join {
  top: 35px;
  left: 45px;
}

.a>.l-1 {
  height: 35px;
  width: 90px;
}

.a>.l-2 {
  top: 45px;
  left: 35px;
  height: 20px;
  width: 50px;
}

/* Big land CE */

.land-big.ce {
  top: 50px;
  left: 100px;
  animation-name: earth-rotation-ce-start, earth-rotation-ce-loop;
  animation-duration: 8000ms, var(--earth-rotation);
  animation-timing-function: linear;
  animation-delay: 0s, 5200ms;
  animation-iteration-count: 1, infinite;
}

.land-big.ce>.land-join {
  top: 40px;
  left: 135px;
}

.land-big.ce>.land-join.j-2 {
  top: -10px;
  left: 105px;
}

.ce>.l-1 {
  height: 40px;
  width: 185px;
}

.ce>.l-2 {
  top: 50px;
  left: 120px;
  height: 30px;
  width: 90px;
}

.ce>.l-3 {
  top: -30px;
  left: 90px;
  height: 20px;
  width: 80px;
}

/* Set of smaller lands */

.land.ne {
  top: 25px;
  left: 95px;
  height: 15px;
  width: 40px;
  animation-name: earth-rotation-ce-start, earth-rotation-ce-loop;
  animation-duration: 8000ms, var(--earth-rotation);
  animation-timing-function: linear;
  animation-delay: 0s, 5200ms;
  animation-iteration-count: 1, infinite;
}

.land.au {
  top: 140px;
  left: 270px;
  height: 30px;
  width: 60px;
  animation-name: earth-rotation-ce-start, earth-rotation-ce-loop;
  animation-duration: 8000ms, var(--earth-rotation);
  animation-timing-function: linear;
  animation-delay: 0s, 5200ms;
  animation-iteration-count: 1, infinite;
}

.land.np {
  background-color: #d0e2ee;
  height: 15px;
  width: 80px;
  top: -3px;
  left: 60px;
}

.land.sp {
  background-color: #d0e2ee;
  height: 15px;
  width: 100px;
  top: 190px;
  left: 50px;
}

/* Set of cloud */

.cloud.c1,
.cloud.c2,
.cloud.c3,
.cloud.c4 {
  height: 13px;
  width: 30px;
}

.cloud.c5,
.cloud.c6 {
  height: 22px;
  width: 63px;
}

.cloud.c7,
.cloud.c8 {
  height: 22px;
  width: 63px;
}

.cloud.c1 {
  top: 35px;
}

.cloud.c2 {
  top: 85px;
  left: -50px;
}

.cloud.c3 {
  top: 100px;
  left: 120px;
}

.cloud.c4 {
  top: 150px;
  left: 160px;
}

.cloud.c5 {
  top: 45px;
  left: 10px;
}

.cloud.c6 {
  top: 115px;
  left: -30px;
}

.cloud.c7 {
  top: 30px;
  left: 120px;
}

.cloud.c8 {
  top: 160px;
  left: 160px;
}

.cloud.c1,
.cloud.c2 {
  animation-name: earth-rotation-cla-start, earth-rotation-cla-loop;
  animation-duration: 28000ms, var(--cloud-rotation);
  animation-timing-function: linear;
  animation-delay: 0s, 28000ms;
  animation-iteration-count: 1, infinite;
}

.cloud.c3,
.cloud.c4 {
  animation-name: earth-rotation-cle-start, earth-rotation-cle-loop;
  animation-duration: 10000ms, var(--cloud-rotation);
  animation-timing-function: linear;
  animation-delay: 0s, 10000ms;
  animation-iteration-count: 1, infinite;
}

.cloud.c5,
.cloud.c6 {
  animation-name: earth-rotation-cla-start, earth-rotation-cla-loop;
  animation-duration: 20000ms, var(--cloud-rotation);
  animation-timing-function: linear;
  animation-delay: 0s, 20000ms;
  animation-iteration-count: 1, infinite;
}

.cloud.c7,
.cloud.c8 {
  animation-name: earth-rotation-cle-start, earth-rotation-cle-loop;
  animation-duration: 10000ms, var(--cloud-rotation);
  animation-timing-function: linear;
  animation-delay: 0s, 10000ms;
  animation-iteration-count: 1, infinite;
}</style>