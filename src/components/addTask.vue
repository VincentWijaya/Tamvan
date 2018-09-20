<template>
  <section class="bg-light content-section pt-3">
    <div class="container">
      <div class="row">
        <div class="col-lg-6 mx-auto text-center">
          <h2 class="section-heading text-dark">Create your task here!</h2>
          <hr class="light my-4">
          <div class="alert alert-warning" id="error" style="display: none">
            
          </div>
          <div class="form-group">
            <form>
              <input type="text" class="form-control" placeholder="Insert your task name" required autocomplete="off">
              <br>
              <input type="text" class="form-control" placeholder="Insert your task description" required autocomplete="off">
              <br>
              <input type="button" class="btn btn-light" value="Submit">
            </form>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
}
</script>

<style>
</style>
