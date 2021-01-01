<template>
  <div class="home">
    <div v-if="projects.length">
      <div v-for="project in projects" :key='project.id'>
        <project_card :project='project' @delete="deleteutil" @complete='completeutil' />
      </div>
    </div>
  </div>
</template>

<script>
import Project_card from '../components/ProjectCard.vue'
export default {
  name: 'Home',
  components: {Project_card},
  data(){
    return{
      projects: [],
    }
  },
  methods:{
    deleteutil(id){
      this.projects= this.projects.filter((project)=>{ return project.id!==id})
    },
    completeutil(id){
      let p= this.projects.find((pr)=>{
        return pr.id===id
      })
      p.complete= !p.complete
    }
  },
  mounted(){
    //fetch the projects
    fetch('http://localhost:3000/projects')
    .then(res => res.json())
    .then(data => this.projects=data)
    .catch(err=> console.warn(err.message))
  }
}
</script>
