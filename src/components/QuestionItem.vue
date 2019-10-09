<template>
    <div class="question-item" v-if="question.id == currentQ">
        <!-- <input type="checkbox" name="" id="" v-model="todo.completed"> -->
        <p class="question" id=''>{{question.question}}</p>
        <button value="true" v-on:click="onCompletedClick('True')">True</button>
        <button value="false" v-on:click="onCompletedClick('False')">False</button>
    </div>
</template>

<script>




export default {
    name: 'QuestionItem',
    props: ['question'],
    data (){
        return {
            currentQ: 0
        }
    },
    created: function() {
    this.$parent.$on('next-question', this.nextQuestion);
    },
    methods: {
        onCompletedClick: function(user_answer, id){
            this.$emit('complete-question', user_answer, this.question.id);
            // currentQ++;
        },

        nextQuestion(id){
            this.currentQ = id;
            console.log(this.currentQ);
            
        }

    }
    
}
</script>

<style scoped>

</style>