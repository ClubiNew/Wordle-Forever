<template>
    <div class="game" v-for="(row, rowIndex) in rows" :key="rowIndex">
        <div class="row" v-for="(letter, letterIndex) in row" :key="letterIndex">
            <div class="letter" :style="{ 'background-color': letter.color, outline: letter.outline }">
                {{ letter.content }}
            </div>
        </div>
    </div>
    <h4 v-if="currentGuess == 6">Correct Answer: {{ word }}</h4>
    <h4 v-if="invalidWord">Not in word list</h4>
    <button class="button" @click="newWord">Next Wordle</button>
</template>

<script>
var answerWords, validWords;

export default {
    name: "Game",

    data() {
        return {
            word: "",
            currentGuess: 0,
            invalidWord: false,
            rows: [],
        };
    },

    methods: {
        newWord() {
            document.activeElement.blur(); // prevent enter key triggering next worlde

            this.word = answerWords[Math.floor(Math.random() * answerWords.length)];
            this.invalidWord = false;
            this.currentGuess = 0;

            for (let r = 0; r < 6; r++) {
                this.rows[r] = [];
                for (let c = 0; c < 5; c++) {
                    this.rows[r][c] = {
                        content: "",
                        color: "rgba(0,0,0,0)",
                        outline: "3px solid rgb(42, 42, 42)",
                    };
                }
            }
        },
    },

    mounted() {
        if (!answerWords || !validWords) return;
        this.newWord();
    },

    async created() {
        answerWords = await fetch("words/answers")
            .then((res) => res.text())
            .then((text) => text.split("\n"));

        validWords = await fetch("words/valid")
            .then((res) => res.text())
            .then((text) => text.split("\n"));

        this.newWord();

        window.addEventListener("keydown", (e) => {
            if (this.currentGuess == 6) return;
            if (e.key == "Enter") {
                let guess = "";
                this.rows[this.currentGuess].forEach((letter) => {
                    guess += letter.content;
                });

                if (guess === "" || validWords.indexOf(guess) < 0) {
                    this.invalidWord = true;
                    return;
                } else {
                    this.invalidWord = false;
                }

                let correctLetters = 0;
                this.rows[this.currentGuess].forEach((letter, index) => {
                    letter.outline = "none";
                    if (letter.content == this.word[index]) {
                        letter.color = "#538d4e";
                        correctLetters += 1;
                    } else if (letter.content != "" && this.word.indexOf(letter.content) >= 0) {
                        letter.color = "#b59f3b";
                    } else {
                        letter.color = "rgb(42,42,42)";
                    }
                });
                if (correctLetters == 5) {
                    this.currentGuess = 6;
                } else {
                    this.currentGuess += 1;
                }
            } else if (e.key == "Backspace") {
                for (let c = 4; c >= 0; c--) {
                    const letter = this.rows[this.currentGuess][c];
                    if (letter.content != "") {
                        letter.outline = "3px solid rgb(42, 42, 42)";
                        letter.content = "";
                        break;
                    }
                }
            } else {
                const charCode = e.key.charCodeAt(0);
                if (charCode >= 97 && charCode <= 122) {
                    for (let c = 0; c < 5; c++) {
                        const letter = this.rows[this.currentGuess][c];
                        if (letter.content == "") {
                            letter.outline = "3px solid rgb(62, 62, 62)";
                            letter.content = e.key;
                            break;
                        }
                    }
                }
            }
        });
    },
};
</script>

<style scoped>
.game {
    width: 100%;
    max-width: 575px;
    margin: auto;
}

.row {
    display: inline-block;
    vertical-align: middle;
}

.letter {
    margin: 3px;
    width: 60px;
    height: 60px;
    line-height: 60px;
    vertical-align: middle;
    font-size: 30px;
    outline-offset: -5px;
}
</style>
