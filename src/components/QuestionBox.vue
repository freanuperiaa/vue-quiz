<template>
    <div class="question-box-container">
        <b-jumbotron lead="Bootstrap v4 Components for Vue.js 2">
                <template v-slot:lead>
                {{ currentQuestion.question }}
                </template>
                <hr class="my-4">
                <b-list-group>
                    <b-list-group-item
                         v-for="(answer, index) in shuffledAnswers" 
                         :key="index"
                         @click="selectAnswer(index)"
                         :class="[selectedIndex === index ? 'selected' : '']"
                    >
                        {{ answer }}
                    </b-list-group-item>
                </b-list-group>

                <b-button variant="primary"
                    @click="submitAnswer"   
                >
                    Submit
                </b-button>
        </b-jumbotron>
    </div>
</template>

<script>
import _ from 'lodash';

export default {
    props: {
        currentQuestion: Object,
        nextQuestion: Function,
        increment: Function,
    },
    data: function() {
        return {
            selectedIndex: null,
            shuffledAnswers: [],
        };
    },
    computed: {
        answers() {
            let answers = [...this.currentQuestion.incorrect_answers];
            answers.push(this.currentQuestion.correct_answer);
            return answers;
        },
        correctAnswer() {
            return this.answers[3];
        }
    },
    watch : {
        currentQuestion: {
            immediate: true,
            handler() {
                this.selectedIndex = null;
                this.shuffleAnswers();
            }
        }
        // 
        // currentQuestion() {
        //     this.selectedIndex = null;
        //     this.shuffleAnswers();
        // }
        // we'll make the currentQuestion into an object having options, so that we can shuffle answers right away
    },
    methods: {
        selectAnswer(index) {
            this.selectedIndex = index;
        },
        shuffleAnswers() {
            let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer];
                this.shuffledAnswers = _.shuffle(answers);
             
        },
        submitAnswer() {
            if (this.selectedIndex === null){
                return
            }
            let isCorrect = false;
            if (this.shuffledAnswers[this.selectedIndex] === this.correctAnswer) {
                isCorrect  = true;
                console.log(isCorrect);
            }
            this.increment(isCorrect);
            this.nextQuestion();
        }
    },
}
</script>

<style scoped>
    .list-group {
        margin-bottom: 15px;
    }
    .list-group-item:hover {
        background: #EEE;
        cursor: pointer;
    }
    .button-next {
        margin-left: 15px;
    }
    .selected {
        background-color: lightblue;
    }
    .correct {
        background-color: lightgreen;
    }
    .incorrect {
        background-color: lightcoral;
    }
</style>