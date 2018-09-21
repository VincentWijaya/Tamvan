<template>
  <div id="app">

    <addTask/>

    <div class="row">
      <card v-for="(cardName, index) in cardNames" :key="index" :name="cardName"/>
    </div>

  </div>
</template>

<script>
import addTask from './components/addTask.vue'
import card from './components/card.vue'
import database from './firebaseConf.js'

const taskData = [
  {
    name: 'Todo',
    data: []
  },
  {
    name: 'On-going',
    data: []
  },
  {
    name: 'Done',
    data: []
  }
]

export default {
  name: 'app',
  data () {
    return {
      cardNames: ['Todo', 'On-going', 'Done']
    }
  },
  components: {
    addTask,
    card
  },
  created() {
    database.ref('/').on('value', (snapshot) => {
      let done = snapshot.val().Kanban.Done
      
      for (let task in done) {
        console.log(task)
      }
    })
  }
}
</script>

<style>
</style>
