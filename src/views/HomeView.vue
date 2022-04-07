<template>
  <layout>
    <div class="container">
      <div class="row align-items-center mt-4">
        <div class="col-12 mt-4">
          <div class="card mt-4">
            <div class="card-body">
              <BaseStepper></BaseStepper>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- <div class="home">
      <img alt="Vue logo" src="../assets/logo.png">
      <HelloWorld msg="Welcome to Your Vue.js App"/>
    </div> -->
  </layout>
</template>

<script>
// @ is an alias to /src
import BaseStepper from '@/components/BaseStepper.vue';
import layout from '@/components/layouts/default.vue';

export default {
  name: 'HomeView',
  components: {
    BaseStepper,
    layout
  }
}
</script>
