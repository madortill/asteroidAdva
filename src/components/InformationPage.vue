<template>
    <div id = "information-page"> 
        <div class = "textInfo"> 
            <h1 class = "textTitle"> {{ astroType[typeAstro].title }} </h1>
            <p class = "infoText"> {{ astroType[typeAstro].text }} </p>
        </div>
        <button class = "retBtn" @click ="prevPage" alt ="retBtn" >חזור</button>
    </div>
</template>

<script>
export default {
    name: "information-page",
    props: ['typeAstro'],
    data() {
        return {
            astroType : [
                {
                    title: 'אסטרואיד בוגר',
                    text: 'אסטרואיד ממש גדול שיכול להשמיד את כדור הארץ'
                },
                {
                    title: 'אסטרואיד נער מתבגר',
                    text: 'אסטרואיד שהוא די חרא כי הוא בכוונה מנסה להפציץ מקומות שהוא לא אוהב '
                },
                {
                    title: 'אסטרואיד בייבי',
                    text: 'אסטרואיד ממש קטן והורס רק שכונות מקומיות'
                }
            ]
        };
    },
    methods: {
        prevPage() {
            this.$emit('prev-page');
        }
    }
};
</script>

<style> 
.retBtn {
    position: fixed;
    font-family: 'Heebo-bold';
    background-color: #61a5c2;
    border-radius: 3vw;
    width: 20vw;
    height: 5.5vh;
    min-width: 20vw;
    max-width: 6vh;
    color: #e6e8d2;
    cursor: pointer;
    top: 70%;
    left: 60%;
    outline: 2px solid #61a5c2;
}

.textTitle {
  font-family: 'Heebo-Bold';
}

.infoText {
    font-size: 1.2rem;
}
</style>
