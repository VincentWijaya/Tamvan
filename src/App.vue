<template>
  <div id="app">

    <addTask/>

    <div class="row">
      <card v-for="(cardName, index) in cardNames" :key="index" :name="cardName" :content="content"/>
    </div>

  </div>
</template>

<script>
import addTask from './components/addTask.vue'
import card from './components/card.vue'
import database from './firebaseConf.js'

export default {
  name: 'app',
  data () {
    return {
      cardNames: ['Todo', 'On-going', 'Done'],
      tasks: []
    }
  },
  components: {
    addTask,
    card
  },
  created () {
    database.ref('/').on('value', (snapshot) => {
      let arr = []

      snapshot.forEach(data => {
        let obj = {
          id: data.key,
          task: data.val().task,
          description: data.val().description,
          status: data.val().status
        }

        arr.push(obj)
      })

      this.tasks = arr
    })
  },
  computed: {
    content () {
      return this.tasks
    }
  }
}
</script>

<style>
</style>
