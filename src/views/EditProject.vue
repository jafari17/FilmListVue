<template>
  <form @submit.prevent="handleEdit" >
    <label>Film:</label>
    <input v-model="film" type="text" required>
    <label>Director:</label>
    <input v-model="director">
    <label>Year:</label>
    <input v-model="year">
    <button>Update Film</button>
  </form>
</template>

<script >
export default {
  props: ['id'],
  data() {
    return {
      film: '',
      director: '',
      year:'',
      uri: "http://localhost:3000/projects/" + this.id,
      project:[]
    }
  },
  mounted() {
    fetch(this.uri)
        .then(res => res.json())
        .then(data => {
          console.log(data)
          this.project = data

          this.film = data.film
          this.director = data.director
          this.year = data.year
        }).catch(err => console.log(err.message))

  },
  methods: {
    handleEdit(){
      fetch(this.uri,{
        method:"PATCH",
        headers:{ 'content-Type': 'application/json'},
        body: JSON.stringify({film: this.film , director:this.director, year:this.year})
      }).then(() => {
         this.$router.push('/')
      }).catch(err => console.log(err.message))
    }
  }
}
</script>


<style scoped>

</style>