<template>
    <div id="game-screen">
        <game-bg-svg @btn-pressed="alert('dfa')" class="svg"></game-bg-svg>
        <div v-if="showGame" class="game-explain">
            <h1>הוראות למשחק</h1>
            <p>הסבר על המשחק</p>
            <button class="btnGame" @click="startGame">התחל המשחק</button>
        </div>
        <div v-if="!showGame" class="fit-content">
            <div v-if="countdown > 0" class="countdown-container">
                <div class="countdown">{{ countdown }}</div>
            </div>
            <div class="grid-container">
                <div v-for="(row, rowIndex) in grid" :key="'row' + rowIndex" class="row">
                    <div v-for="(cell, colIndex) in row" :key="rowIndex + '_' + colIndex" :id="rowIndex + '_' + colIndex"
                        class="cell">{{ cell }}
                        <img :src="asteroidImg" style = ""/>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import gameBgSvg from './gameBgSvg.vue';
import asteroid from '@/assets/asteroid.svg';
export default {
    components: { gameBgSvg },
    name: "game-screen",
    data() {
        return {
            showGame: true,
            countdown: 3,
            asteroidImg: asteroid,
            // matrix: [[false, false, false],
            // [false, false, false],
            // [false, false, false]]
            boardGrid: [],
            rowNum: 4,
            colNum: 3,
            grid: [
                [],
                [],
                [],
                [],
                [],
                [],
                [],
                [],
                [],
                [],
                [],
                [],
            ]
        };
    },
    mounted() {
        this.initGrid();
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
        initGrid() {
            for (let i = 0; i < this.rowNum; i++) {
                const row = [];
                for (let j = 0; j < this.colNum; j++) {
                    row.push(false);
                }
                this.boardGrid.push(row);
            }
            console.table(this.boardGrid);
        }
    },
    computed: {
        
    }
};
</script>

<style>
#game-screen {
    background-repeat: no-repeat;
    background-size: 100% 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    /* Center vertically */
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

.grid-container {
    width: 50vw;
    height: 50vh;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(4, 1fr);
    /* background-color: pink; */
    margin-bottom: 30vh;
    text-align: center;
}

.row {
    display: flex;
    border: 1px solid #ccc;
}

.cell {
    flex: 1;
    border: 1px solid #ccc;
    /* Add borders to cells for visibility */
}

.svg {
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
}

.fit-content {
    height: fit-content;
}
</style>
