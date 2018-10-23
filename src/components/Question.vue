<template>
    <div>
    <p class="question">{{question}}</p>
    <table class="answer-table">
        <tr>
            <td class="answer answer-a" @click="$emit('answered','A')">{{answerA}}</td>
            <td class="answer answer-b" @click="$emit('answered','B')" >{{answerB}}</td>
        </tr>
    </table>
    </div>
</template>

<script>
export default {
  name: "Question",
  props: {
    question: String,
    answerA: String,
    answerB: String
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.answer{
    cursor: pointer;
    height: 20vh;
    width:50%;
    cursor: pointer;
}

.answer-a{
    /* background-color: lightblue; */
    background-color: lightblue;
}

.answer-b{
    /* background-color: lemonchiffon; */
    background-color: lightblue;
}

.question{
    font-weight: bold;
}

.answer-table{
    width:100vw;
    text-align: center;
}
</style>