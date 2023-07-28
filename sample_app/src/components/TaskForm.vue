<template>
  <div>
    <form @submit.prevent="handlEvent">
        <input type="text" placeholder="I would like to...." v-model="newTask">
        <button>Add Task</button>
    </form>
  </div>
</template>

<script>
import { ref } from 'vue';
import { useTaskStore } from '../Stores/TaskStores';

export default {
    setup(){
        const newTask=ref('');
        const taskStore=useTaskStore();

        const handlEvent=()=>{
            if(newTask.value.length>0){
                taskStore.addTask({
                    title:newTask.value,
                    isFav:false,
                    id:Math.floor(Math.random()*100)
                })
            }
            newTask.value='';
        
        }
        return {newTask,handlEvent}
    }
    
}
</script>

