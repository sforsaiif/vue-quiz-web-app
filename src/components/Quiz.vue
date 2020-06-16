<template>
    <div class="container">
        <div class="quizbox">
            <h1 class="question">{{(JSON.stringify(currentQuestion.question))}}</h1>
                <ul class="collection">
                    <li  class="collection-item"
                        v-for="(answer, index) in answers" :key="index"
                        @click.prevent="selectAnswer(index)"
                        :class="[
                            !answered && selectedIndex===index?'selected':
                            answered && correctIndex===index?'green darken-1': 
                            answered && selectedIndex ===index && correctIndex !==index ? 'red darken-1':''

                        ]"


                    >{{answer}}</li>
                </ul>
            <div class="buttons">
                <a class= "waves-effect waves-light btn green"  @click="submitAnswer "  :disabled="selectedIndex===null || answered" ><i class="material-icons left">check</i>Submit</a>
                <a @click="next" class= "waves-effect waves-light btn blue"><i class="material-icons left">navigate_next</i>Next</a>
            </div>
            
        </div>

    </div>

        
</template>

<script>
    import _ from 'lodash';
    export default {

        props:
             {
            currentQuestion:Object,
            next:Function,
            increment:Function,
            
             },

        data(){
            return {
                selectedIndex:null,
                correctIndex:null,
                shuffledAnswers:[],
                answered:false,
            }
        },
        
        computed: {
            answers(){
                let answers=[...this.currentQuestion.incorrect_answers];
                answers.push(this.currentQuestion.correct_answer);
                return answers;
            }

        },

        watch: {
            currentQuestion : {
                immediate:true,
                handler(){
                    this.selectedIndex=null;
                    this.answered=false;
                    this.shuffleAnswers();
                }
            }
        },

        methods: {
            selectAnswer(index){
                this.selectedIndex=index;
            },
            shuffleAnswers() {
                let answers = [...this.currentQuestion.incorrect_answers,this.currentQuestion.correct_answer]
                this.shuffledAnswers=_.shuffle(answers);
                this.correctIndex=this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
            },

            submitAnswer() {
                this.countIndex++;
                let isCorrect=false;
                if(this.selectedIndex===this.correctIndex){
                    isCorrect=true;
                }
                this.answered=true;
                this.increment(isCorrect)
                
            },


            }


    }

</script>

<style scoped>
.quizbox{
    width:500px;
    margin:0 auto;
}

.question{
    font-size:28px;
    padding-top:40px;
}

.buttons {
    text-align:center;
}

.btn {
    margin-left:15px;
}

.collection-item{
    cursor:pointer;
}

.collection-item:hover{
    background-color:#FFFFAA;
}

.selected{
    background-color:#FFFFAA;
}

.correct {
    background-color:green;
    color:white;
}

.wrong {
    background-color:red;
    color:white;
}


@media only screen and (max-width: 600px) {
    .quizbox {
        width:90%;
    }

    .question{
        font-size:1.6rem;
    }

    .btn{
        margin:15px;
    }
  }
</style>