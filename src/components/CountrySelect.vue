<template>
  <!--Since it's input field, we want to bind to the data so we added v-model   -->
  <select 
  @change="onChange()"
  v-model="selected" class="form-select mt-10 block w-full border p-3 rounded drop-shadow-md cursor-pointer bg-slate-100">
    <!-- countries being passed in as props  -->
    <option value="0">Select Country: </option>
      <!-- v-for to loop through the array of countries -->
      <option v-for="country in countries" v-bind:value="country.ID" :key="country.ID">
       {{ country.Country }}  </option>  
  </select>

  <!-- <a href="#" class="group block max-w-xs mx-auto rounded-lg p-6 bg-white ring-1 ring-slate-900/5 shadow-lg space-y-3 hover:bg-sky-500 hover:ring-sky-500">
  <div class="flex items-center space-x-3">
    <svg class="h-6 w-6 stroke-sky-500 group-hover:stroke-white" fill="none" viewBox="0 0 24 24">...</svg> -->
    <!-- <h3 class="text-slate-900 group-hover:text-white text-sm font-semibold">New project</h3>
  </div>
  <p class="text-slate-500 group-hover:text-white text-sm">Create a new project from a variety of starting templates.</p>
</a> -->
</template>


<script>
export default {
  name: 'CountrySelect',
  props: ['countries'],
  // v-bind the data with the data object
  data() {
    return {
      selected: 0
    }
  },
  methods: {
    // emit the change event up to the Home because we will need to change the stats based on Country selected
    onChange() {
      const country = this.countries.find((item)=> item.ID === this.selected)

      console.log(country);
      // passing variable country up to Home
      this.$emit('get-country', country);
    }
  }
}
</script>