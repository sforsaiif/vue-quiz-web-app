<template>
<div>
    <nav class="green darken-1">
    <div class="nav-wrapper container">
      <a href="." class="brand-logo">QuizZz</a>
      <ul  class=" hide-on-small-only right">
        <li class="count"><i class="material-icons left">timer</i>Count: {{numCorrect}}/{{numTotal}}</li>
      </ul>
    </div>
  </nav>

<ul  class="screen-small hide-on-med-and-up">
        <li>COUNT: {{numCorrect}}/{{numTotal}}</li>
</ul>

</div>
</template>

<script>
  export default {
    props: [
      'numCorrect',
      'numTotal'
    ]
  }
</script>

<style scoped>
.brand-logo {
  font-weight:bold;



}

.count {
    font-size:18px;
    margin-left:40px;
}


@media only screen and (max-width: 600px) {
    .screen-small{
      text-align:center;
    }

    .screen-small li{
      margin-top:30px;
      font-size:1.7rem;
    }
}

</style>