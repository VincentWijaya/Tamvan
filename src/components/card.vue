<template>
  <div class="col-sm-3 my-5 mx-auto">
    <div class="card">
      <div class="card-body">
        <h4 class="card-title text-center">{{ name }}</h4>
        <contentCard :cardName="name" :content="content"/>
      </div>
    </div>
  </div>
</template>

<script>
import contentCard from './contentCard.vue'

export default {
  props: ['name', 'content'],
  components: {
    contentCard
  }
}
</script>
