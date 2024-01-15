<template>
    <div id = "asteroid-type"> 
        <div class = "infoType"> 
            <div v-if = "!showInfo"> 
                <p class ="text"> לחצו עליי וגלו איזה אסטרואיד אני.</p>
                <div class="asteroid-container" @click="moveToNext"> 
                    <img id = "adult-Asteroid" class="Asteroid" src = "@/assets/moon.svg" alt = "adult-Asteroid">
                    <img id ="baby-Asteroid" class="Asteroid" src = "@/assets/moon.svg" alt = "baby-Asteroid">
                    <img id ="teenage-Asteroid" class="Asteroid" src = "@/assets/moon.svg" alt = "teenage-Asteroid">
                </div>
                <button class = "btnPerv" @click ="prevPage">חזור</button>
                <button v-if = "btnClick >= 3 && !showInfo" @click = statGame class = "btnPerv">למשחק</button>
            </div>   
            <div v-if = "showInfo"> 
                    <information-page :typeAstro = typeAstro @prev-page = prevTypePage></information-page>
            </div>
        </div>
    </div>
</template>

<script>
import InformationPage from '@/components/InformationPage.vue';

export default {
    name: "asteroid-type" ,
    components: {
        InformationPage,
    },
    data() {
        return {
            btnClick: 0,
            showInfo: false,
            typeAstro: 0,
        };
    },
    methods: { 
        moveToNext(event) {
            if(event.target.tagName === "IMG") {
                this.btnClick++;
                this.showInfo = true;
                if(event.target.id === "baby-Asteroid") {
                    this.typeAstro = 2;
                } else if(event.target.id === "teenage-Asteroid"){
                    this.typeAstro = 1;
                } else {
                    this.typeAstro = 0;
                }
            }
        },
        prevPage() {
            this.$emit('prev-page');
        },
        prevTypePage() {
            this.showInfo = false;
        },
        statGame() {
            this.$emit('start-game');
        }
    }
};
</script>

<style> 
* {
    color: #e6e8d2;
}
#asteroid-type {
    background-image: url("@/assets/bgOpenScreen.svg");
    background-repeat:no-repeat;
    background-size: 100% 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    width: 100vw;
}

.infoType {
    text-align: center;
    background-repeat:no-repeat;
    background-size: cover;
    height: 70%;
    width: 65%;
    border-radius: 10%;
}
.btnPerv {
    position: fixed;
    left: 25%;
    top: 70%;
    font-family: 'Heebo-bold';
    background-color: #61a5c2;
    border-radius: 3vw;
    width: 20vw;
    height: 5.5vh;
    min-width: 20vw;
    max-width: 6vh;
    color: #e6e8d2;
    cursor: pointer;
    outline: 2px solid #61a5c2;
}


.btnCon:active {
    background-color: #71b3ec;
}

#baby-Asteroid {
    width: 30%;
    cursor: pointer;
    align-self: flex-end;
}
#teenage-Asteroid {
    width: 40%;
    cursor: pointer;
}
#adult-Asteroid {
    width: 60%;
    cursor: pointer;
}

.Asteroid {
    cursor: pointer;
    flex-shrink: 0;
    min-height: 55px;
    min-width: 55px;
}

.asteroid-container {
    animation: floatAnimation 2s ease-in-out infinite;
    display: flex;
    flex-direction: column;
    margin-top: 40%;
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

.text {
    position: fixed;
    font-size: 1.1rem;
    padding: 35%;
    bottom: 37%;
    right: 23%;
}
</style>