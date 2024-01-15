<template>
    <div id="game-screen">
        <game-bg-svg @btn-pressed="alert('dfa')" class="svg"></game-bg-svg>
        <div v-if="showGame" class="game-explain">
            <h1>הוראות למשחק</h1>
            <p>הסבר על המשחק</p>
            <button class="btnGame" @click="startGame">התחל המשחק</button>
        </div>
        <div v-if="!showGame" class="fit-content">
            <p v-show="showAnswer" class="textAnswer" :class="indexAnswer === 0 ? 'right-answer' : 'wrong-answer'"> {{
                arrayText[indexAnswer] }}</p>
            <div v-if="showCoordinates" class="coordinates">
                <p>:הקואורדינטה היא</p>
                <p class="textNum"> {{ randomAnswer.replaceAll("_", ",") }} </p>
            </div>
            <div v-if="countdown > 0" class="countdown-container">
                <div class="countdown">{{ countdown }}</div>
            </div>
            <div class="grid-container" @click="checkAnswer">
                <div v-for="(row, rowIndex) in rowNum" :key="'row' + rowIndex" class="row">
                    <div v-for="(cell, colIndex) in colNum" :key="rowIndex + '_' + colIndex" :id="rowIndex + '_' + colIndex"
                        class="cell" :class="showGrid === false ? 'disabledGrid' : 'regularGrid'">
                    </div>
                </div>
            </div>
            <button class="btnHelp" @click="btnShowGrid" :class="indexBtn >= 6 ? 'disabled' : 'regular'"> ? </button>
        </div>
        <div v-if="showEndSCreen">
            <!-- <end-screen> </end-screen> -->
        </div>
    </div>
</template>

<script>
import gameBgSvg from './gameBgSvg.vue';
import asteroid from '@/assets/asteroid.svg';
// import EndScreen from '@/EndScreen.vue';
export default {
    components: {
        gameBgSvg,
        // EndScreen
    },
    name: "game-screen",
    data() {
        return {
            showGrid: false,
            showCoordinates: false,
            indexBtn: 0,
            showGame: true,
            showAnswer: false,
            showEndSCreen: false,
            countdown: 3,
            asteroidImg: asteroid,
            randomRow: 0,
            randomCol: 0,
            randomAnswer: "",
            rowNum: 4,
            colNum: 3,
            myTimer: 0,
            score: 0,
            lose: 0,
            indexAnswer: 0,
            arrayText: [
                "תשובה נכונה",
                "תשובה לא נכונה"
            ],
        };
    },
    mounted() {
        this.myTimer = setTimeout(this.randomNumbers, 5500);
    },
    methods: {
        startGame() {
            this.showGame = false;
            this.startCountdown();
        },
        startCountdown() {
            const timer = setInterval(() => {
                if (this.countdown > 1) {
                    this.countdown--;
                } else {
                    clearInterval(timer);
                    this.countdown = -1;
                }
            }, 1000);
        },
        randomNumbers() {
            this.showCoordinates = true;
            this.randomRow = Math.round(Math.random() * (3 - 0)) + 0;
            this.randomCol = Math.round(Math.random() * (2 - 0)) + 0;
            this.randomAnswer = `${this.randomRow}_${this.randomCol}`;
            setTimeout(() => {
                this.showCoordinates = false;
            }, 2000);
        },
        btnShowGrid() {
            this.indexBtn++;
            if (this.indexBtn < 7) {
                if (this.indexBtn % 2 == 0) {
                    this.showGrid = false;
                } else {
                    this.showGrid = true;
                }
            }
        },
        checkAnswer(event) {
            const userAnswer = event.target.id;
            console.log(userAnswer);
            console.log(this.randomAnswer);
            setTimeout(() => {
                this.showAnswer = false;
            }, 1500)
            this.showAnswer = true;
            if (userAnswer === this.randomAnswer) {
                this.myTimer = setTimeout(this.randomNumbers, 2000);
                console.log("you right");
                this.score++;
                this.indexAnswer = 0;
            } else {
                console.log("you wrong");
                this.indexAnswer = 1;
                this.myTimer = setTimeout(this.randomNumbers, 2000);
                if (this.score > 0) {
                    this.score--;
                    this.lose++;
                }

            }

            if (this.lose === 3) {
                console.log("lose");
            }

            if (this.score === 3) {
                console.log("win");
            }

        },
    },
};
</script>

<style>
#game-screen {
    direction: ltr;
    background-repeat: no-repeat;
    background-size: 100% 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    width: 100vw;
    padding-top: 10vw;
    position: relative;
}

.game-explain {
    width: 80%;
    height: 80%;
    background-color: #013a63;
    border-radius: 10px;
    text-align: center;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    z-index: 1;
    position: relative;
}

.textNum {
    font-size: 2rem;
    /* Adjust the font size as needed */
    color: #fff;
}

.countdown-container {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}

.countdown {
    font-size: 8rem;
    color: cornsilk;
}

.btnGame {
    background-color: #61a5c2;
    border-radius: 3vw;
    color: #e6e8d2;
    cursor: pointer;
    font-family: 'Heebo-bold';
    height: 5.5vh;
    min-width: 30vw;
    max-width: 6vh;
    outline: 2px solid #61a5c2;
}

.regularGrid {
    opacity: 100%;
}

.disabledGrid {
    opacity: 0%;
}

.btnHelp {
    position: fixed;
    top: 72%;
    left: 9%;
    /* Adjust the left position as needed */
    transform: translate(-50%, -50%);
    width: 50px;
    /* Adjust the width as needed */
    height: 50px;
    border-radius: 50%;
    color: #fff;
    background-color: #61a5c2;
    border: none;
    cursor: pointer;
    font-size: 1rem;
    z-index: 2;
}

.disabled {
    background-color: rgba(254, 250, 224, 0.411);
    color: rgb(196, 194, 177);
}

.regular {
    background-color: rgb(254, 250, 224);
    color: rgb(40, 54, 24);
}

.coordinates {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 75vw;
    height: 30vh;
    background-color: #1c2a69;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    z-index: 2;
}

.grid-container {
    position: relative;
    z-index: 1;
    width: 50vw;
    height: 50vh;
    display: grid;
    grid-template-columns: repeat(v-bind(colNum), 1fr);
    grid-template-rows: repeat(v-bind(rowNum), 1fr);
    margin-bottom: 30vh;
    text-align: center;
    /* position: absolute; */
}

.row {
    display: contents;
    cursor: pointer;
}

.cell {
    flex: 1;
    border: 1px solid #ccc;
}


.svg {
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    z-index: -1;
}

.textAnswer {
    text-align: center;
    font-size: 1.3rem;
}

.wrong-answer {
    color: red;
}

.right-answer {
    color: #a7c957;
}
</style>
