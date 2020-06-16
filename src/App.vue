<template>
  <div id="app">
    <Navbar :numCorrect="numCorrect"
            :numTotal="numTotal"
     />
     <div v-if="index<=9">
    <Quiz 
     :currentQuestion="questions[index]"
     :next="next"
     :increment="increment"
     :countIndex="countIndex"
    
    />
    </div>

    <div v-else>
      <Endbox />
    </div>
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue';
import Quiz from './components/Quiz.vue';
import Endbox from './components/Endbox.vue';

export default {
  name: 'App',
  components: {
    Navbar,
    Quiz,
    Endbox,
  },

  data(){
    return {
      questions: [],
      index:0,
      numCorrect:0,
      numTotal:0,
    }

  },

  methods: {
    next(){
      this.index++;
    },

    increment(isCorrect){
      if(isCorrect){
        this.numCorrect++;
      }
      this.numTotal++;
    }
  },
  mounted: function(){
    fetch("https://opentdb.com/api.php?amount=10", {
      method: "get"
      })
      .then(response=> {
        return response.json()
      .then(jsonData=>{
        this.questions=jsonData.results;
        console.log(this.questions);
      })
      })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  
}
</style>
