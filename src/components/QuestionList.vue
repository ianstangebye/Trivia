<template>
    <div class="question-list">
        <QuestionItem v-if="questionsList" v-for="question in questions" :key="question.question" v-bind:question="question" v-on:complete-question="completeQuestion"></QuestionItem>
        <img v-if="trophy" alt="trophy" src="https://advantagetrophy.com/wp-content/uploads/2019/05/advantage-trophy-logo.png"/>
        <img v-if="gameOver" alt="lost game" src="https://s.pngix.com/pngfile/s/81-818978_report-abuse-png-transparent-game-over-png-png.png" />
    </div>
</template>

<script>
import QuestionItem from './QuestionItem';
import { log } from 'util';
import axios from 'axios';


export default {
    name: 'QuestionList',
    components: {
        QuestionItem
        },
    async beforeCreate(){
       await axios.get(['https://opentdb.com/api.php?amount=10&type=boolean']).then(resp=>resp.data).then(resp=>{
            console.log(resp.results);
            this.questions = resp.results;
            for(let i=0; i<this.questions.length; i++){
                this.questions[i].id = i;
                this.answers.push(this.questions[i].correct_answer);
                // console.log(answers[i]);
            }
            console.log(this.answers); 

            

            
            
            
        });
 
            
    },
    data(){
        return {
            questions: [],
            answers: [],
            userAnswers: [],
            questionsList: true,
            trophy: false,
            gameOver: false
        }
        // var answers = [];
        
    },
    methods: {
        completeQuestion(user_answer, id){

            // answers[id] = questions[id].correct_answer; 
            // console.log(user_answer);
             console.log(this.answers);
                
             console.log(this.userAnswers);


            if(this.answers[id] == user_answer){
                this.userAnswers.push(true);
                
            } else{
                this.userAnswers.push(false);
            }
            // answers.push(user_answer);
            this.nextQuestion(id);
            
        },
        nextQuestion(id){
            var numOfCorrect =[];
            if(this.userAnswers.length <10){
                this.$emit('next-question', id +1);
                
            } else {
                this.questionsList = false;

                for(let i=0; i<10;i++){
                    if(this.userAnswers[i] == true){
                        numOfCorrect.push(this.userAnswers[i]);
                    }
                }

                
                console.log(numOfCorrect.length);
                    

                if(numOfCorrect.length<5){
                    this.gameOver = true;
                } else if (numOfCorrect.length>5) {
                    this.trophy = true;
                }
            }
        }
    }


}
</script>