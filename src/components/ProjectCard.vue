<template>
 <div class="project" @click="togglecard">
     <div class="actions">
         <h3>{{project.title}}</h3>
     </div>
     <div class="details" v-if="showcard">
         <p>{{project.details}}</p>
     </div>
 </div>
</template>

<script>
export default {
    props: ['project'],
    data(){
        return{
            showcard: false,
        }
    },
    methods:{
        togglecard(){
            this.showcard= !this.showcard
        }
    }
}
</script>

<style>
 .project{
     margin: 20px auto;
     padding: 10px 20px;
     background: white;
     border-radius: 4px;
     box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
     border-left: 4px solid #e90074;
 }
 h3{
     cursor: pointer;
 }
 .details{
     margin: auto;
 }
</style>