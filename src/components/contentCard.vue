<template>
  <div>
      <div class="card-block" v-for="(data, index) in content" :key="index" v-if="data.status === cardName">
        <div class="card my-3">
          <div class="card-body">
            <h5 class="card-title ">{{  data.task }}</h5>
            <hr class="light my-4">
            <h6>{{ data.description }}</h6>
            <hr class="light my-4">
            <div class="d-flex justify-content-between">
              <button type="button" class="btn btn-sm btn-light" v-if="cardName !== 'Todo'" @click="prev(data.id, data.status, data.task, data.description)"><i class="fas fa-less-than"></i></button>
              <div>
                <button type="button" class="btn btn-sm btn-light" v-if="cardName === 'Done'" @click="remove(data.id)"><i class="fas fa-trash"></i></button>
              </div>
              <button type="button" class="btn btn-sm btn-light" v-if="cardName !== 'Done'" @click="next(data.id, data.status, data.task, data.description)"><i class="fas fa-greater-than"></i></button>
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
    prev (id, status, task, description) {
      if (status === 'Done') {
        database.ref(`/${id}`).set({
          task: task,
          description: description,
          status: 'On-going'
        })
      } else if (status === 'On-going') {
        database.ref(`/${id}`).set({
          task: task,
          description: description,
          status: 'Todo'
        })
      }
    },
    next (id, status, task, description) {
      if (status === 'Todo') {
        database.ref(`/${id}`).set({
          task: task,
          description: description,
          status: 'On-going'
        })
      } else if (status === 'On-going') {
        database.ref(`/${id}`).set({
          task: task,
          description: description,
          status: 'Done'
        })
      }
    },
    remove (id) {
      database.ref(`/${id}`).set({})
    }
  }
}
</script>
