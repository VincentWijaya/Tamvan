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
import firebase from 'firebase'

const database = firebase.database()

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
  created () {
    let kanban = database.ref('Kanban')

    kanban.on('value', (snapshot) => {
      console.log(snapshot.val())
    })
  }
}
</script>

<style>
</style>
