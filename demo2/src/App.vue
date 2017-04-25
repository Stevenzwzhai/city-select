<template>
    <div id="app">
        <DistrictSelect></DistrictSelect>
    </div>
</template>

<script>

    import DistrictSelect from './components/DistrictSelect'
    import Vue from 'vue'
    Vue.use(DistrictSelect)
export default {
    name: 'app',
    data () {
      return {
          msg: 'Welcome to Your Vue.js App'
      }
   }
}
</script>

<style>

</style>
