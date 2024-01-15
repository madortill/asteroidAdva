<template>
    <div id="open-screen">
        <div class="part-one">
            <h1 class="textInfo textTitle">{{ titleArray[indexInfo] }}</h1>
            <p class="textInfo"> {{ textArray[indexInfo] }} </p>
            <div class="button-container "> 
                <button  class="btnCon btnContinue " @click="nextPage">המשך</button>
                <button v-if="indexInfo > 0" class="btnCon btnBack" @click="prevPage">חזור</button>
            </div>
        </div>
    </div>
</template>

<script>


export default {
    name: "open-screen",
    data() {
        return {
            indexInfo: 0,
            titleArray: [
                'פתיח הלומדה',
                'מהו אסטרואיד?',
                'פיצוץ אסטרואיד',
                'סוגי אסטרואיד'
            ],
            textArray: [
                'הינכם עומדים לעבור לומדה חשובה מאוד שתכריע אם תהיו אסטרונאוטים טובים או לא. לכן התייחסו אליה ברצינות!',
                'אסטרואיד הוא יצור מרושע שמטרתו להשמיד את כדור הארץ ואנחנו בברוגז איתו. הוא נראה כמו כדור עגול כזה אבל לא חלק כי יש לו בליטות מכוערות שנראות כמו חצקונים.',
                'שיעור פיצוץ אסטרואיד ידוע בחשיבותו בגלל הסכנה היומיומית הנשקפת לכדור הארץ בלעדיו. עשרות אלפי אסטרואידים נעים ברגע זה לכיוון הכוכב שלנו, ועליכם לדעת כיצד למנוע מהם להגיע אלינו',
                'במסך הבא נלמד על סוגי האסטרואידים השונים וחשיבותיהם',
            ],

        };
    },
    methods: {
        nextPage() {
            if (this.indexInfo < 3) {
                this.indexInfo++;
            } else if (this.indexInfo === 3) {
                this.$emit('next-page');
            }
        },
        prevPage() {
            if (this.indexInfo > 0) {
                this.indexInfo--;
            }
        }
    }
};
</script>

<style>
#open-screen {
    background-image: url("@/assets/bgOpenScreen.svg");
    background-repeat: no-repeat;
    background-size: 100% 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    width: 100vw;
}

.part-one {
    text-align: center;
    margin: auto;
    background-repeat: no-repeat;
    height: 60%;
    width: 65%;
    background-size: cover;
    border-radius: 10%;
   
}

.textInfo {
    color: #e6e8d2;
    text-align: center;
    font-size: 1.2rem;
}

.textTitle {
    font-family: 'Heebo-Bold';
    font-size: 2rem;

}

.btnCon {
    cursor: pointer;
    background-color: #61a5c2;
    border-radius: 3vw;
    color: #e6e8d2;
    font-family: 'Heebo-bold';
    height: 5.5vh;
    min-width: 20vw;
    max-width: 6vh;
    position: absolute;
    outline: 2px solid #61a5c2;
}
.btnBack {
    right: 20%;
}

.btnContinue {
  left: 20%;
}
.button-container {
  display: flex;
  justify-content: space-between; /* Distribute space between buttons */
  /* margin-top: 25%; */
}
</style>
  
   