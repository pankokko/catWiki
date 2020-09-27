<template>
<div class="container">
    <div>
    <div class="text-center">
        <alert :alert="alert" :wikipedia-url="expectAnswer.wikipedia_url"></alert>
        <div class="card">
        <div class="card-content">
            <div class="media">
                <div class="media-content">
                <p class="title is-4">Cats Quiz</p>
                <p class="title is-4"> {{ expectAnswer.name }} is from ... </p>
                <div>
                    <div class="field"   
                        v-for="cat in cats[1].otherCatsForQuiz" 
                        :key="cat.id">
                        <b-radio v-model="quiz.radio"
                        name="name"
                        :native-value="cat.origin">
                        {{ cat.origin }}
                        </b-radio>
                    </div>
                    <div class="buttons" v-show="isSelected">
                        <b-button expanded type="is-primary" @click="postAnswer(quiz.radio)">Answer</b-button>
                    </div>
                </div>
            </div>
        </div>
    </div>
    </div>
    </div>
    </div>
</div>
</template>

<script>
import alert from '~/components/Alert.vue'
import AnswerButton from '~/components/AnswerButton.vue'
export default {
    components: {
        alert,
        AnswerButton,
    },
    props: ['cats'], 
    data() {
        return {
            quiz: {
                radio: false,
                submitButton: false,
            },
            alert: {
                correct: false,
                inccorect: false,
                alertMessage: '',
            },
            expectAnswer: {
                name: 'default',
            },
        }
    },
    computed: {
        isSelected(){
            if(this.quiz.radio){
               return this.quiz.submitButton = true
            }
        },
    },
    mounted(){
        this.expectAnswer = this.cats[0]
        console.log(this.expectAnswer)
        this.cats[1].otherCatsForQuiz.push(this.expectAnswer)
    },
    methods: {
        postAnswer(answer){
            this.alert.status = true
            this.alert.correct = false
            this.alert.inccorect  =  false
            if (answer === this.expectAnswer.origin) {
                this.alert.correct = true,
                this.alert.alertMessage = 'correct！'
            } else {
                this.alert.inccorect = true,
                this.alert.alertMessage = 'incorrect'
            }
            this.quiz.submitButton = false
            this.quiz.radio = false
        },
    },
}
</script>
