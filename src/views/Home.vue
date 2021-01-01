<template>
  <div class="home">
    <div v-if="projects.length">
      <div v-for="project in projects" :key='project.id'>
        <project_card :project='project' />
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
  mounted(){
    //fetch the projects
    fetch('http://localhost:3000/projects')
    .then(res => res.json())
    .then(data => this.projects=data)
    .catch(err=> console.warn(err.message))
  }
}
</script>
