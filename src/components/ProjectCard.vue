<template>
 <div class="project">
     <div class="actions">
         <h3 @click="togglecard">{{project.title}}</h3>
         <div class="icons">
             <span class="material-icons">edit</span>
             <span @click="deleteproject" class="material-icons">delete</span>
             <span @click="togglecomplete" class="material-icons">done</span>
         </div>
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
            urldel: "http://localhost:3000/projects/"+ this.project.id,
        }
    },
    methods:{
        togglecard(){
            this.showcard= !this.showcard
        },
        deleteproject(){
            //do a delete request to the database
            fetch(this.urldel,{method: 'DELETE'})
            .then(() =>{this.$emit('delete', this.project.id)})
            .catch(err => console.log(err.message))
        },
        togglecomplete(){
            //do a patch request because it is used for updation
            fetch(this.urldel,{
                method: 'PATCH',
                headers: {'content-Type': 'application/json'},
                body: JSON.stringify({complete: !this.project.complete})
            }).then(()=> this.$emit('complete', this.project.id))
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
.actions{
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.material-icons{
    font-size: 24px;
    margin: 0 10px;
    color: #bbb;
    cursor: pointer;
}
.material-icons:hover{
    color: #777;
}
</style>