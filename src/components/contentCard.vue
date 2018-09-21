<template>
  <div>
      <div class="card-block" v-for="(data, index) in content" :key="index" v-if="data.status === cardName">
        <div class="card my-3">
          <div class="card-body">
            <h5 class="card-title ">{{  data.task }}</h5>
            <hr class="light my-4">
            <h6>Description: {{ data.description }}</h6>
            <h6>Assign to: {{ data.assign }}</h6>
            <hr class="light my-4">
            <div class="d-flex justify-content-between">
              <button type="button" class="btn btn-sm btn-light" v-if="cardName !== 'Back-log'" @click="prev(data.id, data.status, data.task, data.description, data.assign)"><i class="fas fa-less-than"></i></button>
              <div>
                <button type="button" class="btn btn-sm btn-light" @click="remove(data.id)"><i class="fas fa-trash"></i></button>
              </div>
              <button type="button" class="btn btn-sm btn-light" v-if="cardName !== 'Done'" @click="next(data.id, data.status, data.task, data.description, data.assign)"><i class="fas fa-greater-than"></i></button>
            </div>
          </div>
        </div>
      </div>
  </div>
</template>

<script>
import database from '../firebaseConf.js'

export default {
  props: ['content', 'cardName'],
  methods: {
    prev (id, status, task, description, assign) {
      if (status === 'Done') {
        database.ref(`/${id}`).set({
          task: task,
          description: description,
          assign: assign,
          status: 'On-going'
        })
      } else if (status === 'On-going') {
        database.ref(`/${id}`).set({
          task: task,
          description: description,
          assign: assign,
          status: 'Todo'
        })
      } else if (status === 'Todo') {
        database.ref(`/${id}`).set({
          task: task,
          description: description,
          assign: assign,
          status: 'Back-log'
        })
      }
    },
    next (id, status, task, description, assign) {
      if (status === 'Todo') {
        database.ref(`/${id}`).set({
          task: task,
          assign: assign,
          description: description,
          status: 'On-going'
        })
      } else if (status === 'On-going') {
        database.ref(`/${id}`).set({
          task: task,
          assign: assign,
          description: description,
          status: 'Done'
        })
      } else if (status === 'Back-log') {
        database.ref(`/${id}`).set({
          task: task,
          assign: assign,
          description: description,
          status: 'Todo'
        })
      }
    },
    remove (id) {
      database.ref(`/${id}`).set({})
    }
  }
}
</script>
