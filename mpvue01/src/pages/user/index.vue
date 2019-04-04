<template>
  <div>
    <ul>
      <li v-for="item in list">
        {{item}}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  components: {

  },

  data () {
    return {
        list:[],
    }
  },

  created () {
    for(var i=0;i<10;i++){
      this.list.push ("这是第"+i)
    }
}
}
</script>

<style>
</style>
