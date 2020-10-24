<template>
  <div>
    <h1>{{ place }}</h1>
  </div>
</template>


<script>
export default {
    props: {
      place: {
        position: {
          lat: Number, 
          lng: Number
        },
        icon: String,
        title: String,
      }
    },
    data () {
      return{
      }
    },
    watch: {
      placemarker: function(newVal, oldVal) { // watch it
        console.log('Prop changed: ', newVal, ' | was: ', oldVal)
      },
      showInfo: function(newVal, oldVal) {
        console.log('Prop changed: ', newVal, ' | was: ', oldVal)
      }
    }
}
</script>

<style scoped>
</style>