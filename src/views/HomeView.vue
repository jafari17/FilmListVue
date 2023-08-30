<template>
  <div class="home">
    <FilterNav @filterChange="current = $event" :current="current" />
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <SingleProject :project="project" @delete="handelDelete" @star="handelcomplete" />
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import SingleProject from '../components/SingleProject.vue'
import FilterNav from "@/components/FilterNav.vue";

export default {
  name: 'HomeView',
  components: {FilterNav, SingleProject},
  data(){
    return {
      projects: [],
      current: 'all'
    }
  },
  mounted(){
    fetch('http://localhost:3000/projects')
        .then(res => res.json())
        .then(data => this.projects = data)
        .catch(err => console.log(err.message))
  },
  methods:{
    handelDelete(id){
      this.projects = this.projects.filter(item =>{
        return item.id !== id
      })
    },
    handelcomplete(id){
      let p = this.projects.find(item => {
        return item.id === id
      })
      p.star = !p.star
    }
  },
  computed:{
    filteredProjects(){
      if(this.current === 'star'){
        return this.projects.filter(item => item.star)
      }
      else if (this.current === 'non-star'){
        return this.projects.filter(item => !item.star)
      }
      else {
        return this.projects
      }
    }
  }

}
</script>
