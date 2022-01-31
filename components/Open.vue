<template>
  <div class="container bootstrap snippets bootdey">
    <div
      v-for="(question, index) in questionsList"
      :key="index"
      class="row"
    >
      <div class="col-md-12">
        <div class="widget lazur-bg p-xl">
          <h2>{{ index }} - {{ question.question }}</h2>
          <ul
            v-for="(answer, index2) in [...question.incorrect_answers, question.correct_answer].sort()"
            :key="index2"
            class="list-unstyled m-t-md"
          >
            <li>
              <span class="fa fa-envelope m-r-xs" />
              <label>Option {{ index2 }}:  {{ answer }}</label>
              <label v-if="answer === question.correct_answer">Correcto answer!</label>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'OpenPage',
  data () {
    return {
      questionsList: []
    }
  },
  created () {
    this.getDB()
  },
  methods: {
    getDB () {
      fetch('https://opentdb.com/api.php?amount=10')
        .then(response => response.json())
        .then((data) => {
          this.questionsList = data.results
        })
    }
  }
}
</script>

<style scoped>
body{margin-top:20px;}

.p-xl {
  padding: 40px;
}

.lazur-bg {
  background-color: #23c6c8;
  color: #ffffff;
}

.red-bg {
  background-color: #ed5565;
  color: #ffffff;
}

.navy-bg {
  background-color: #1ab394;
  color: #ffffff;
}

.yellow-bg {
  background-color: #f8ac59;
  color: #ffffff;
}

.widget {
  border-radius: 5px;
  padding: 15px 20px;
  margin-bottom: 10px;
  margin-top: 10px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.16), 0 2px 10px rgba(0, 0, 0, 0.12);
}

.widget h2, .widget h3 {
  margin-top: 5px;
  margin-bottom: 0;
  border-bottom:1px dotted white;
}

.m-t-md {
  margin-top: 20px;
}
</style>
