<template>
  <div class="text-center">
    <h2 class="text-3xl font-bold">{{ text }}</h2>
    <div class="text-2xl mt-4 mb-10">
      {{ timestamp }}
    </div>
  </div>
</template>

<script>
import moment from 'moment';

  export default {
    name: 'DataTitle',
    props: ['text', 
    'dataDate'],
    // To happen automatically with a function from moment package
    computed: {
      timestamp: function() {
        // return the dataDate formatted as we needed 
        return moment(this.dataDate).format('MMMM Do YYYY, h:mm:ss a')
      }
    }
  }
</script>