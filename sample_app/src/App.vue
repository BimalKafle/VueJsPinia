<script>
import {useTaskStore} from './Stores/TaskStores.js'
import TaskList from './components/TaskList.vue'
import TaskForm from './components/TaskForm.vue'
import { ref } from 'vue';
export default{
  components:{TaskList,TaskForm},
  setup(){
    const taskStore=useTaskStore();
    const filter=ref('all');
    return {taskStore,filter};
  }
}
</script>

<template>
  <div>
    <main>
      <header>
        <img src="./assets/logo.svg" alt="pinia logo">
        <h1>Pinia Task</h1>
      </header>
       <div class="new-task-form">
          <TaskForm />
       </div>
       <nav class="filter">
        <button @click="filter='all'">All Task</button>
        <button @click="filter='fav'">Favorites</button>
       </nav>
        <div class="task-list" v-if="filter==='all'">
           <p>You have {{taskStore.totalCount}} tasks left to do.</p>
               <div v-for="task in taskStore.tasks" :key="task.id">
                <TaskList :task='task'/>
              </div>
        </div>
          
          <div class="task-list" v-if="filter==='fav'">
            <p>You have {{taskStore.favCount}} favorite tasks lefts to do.</p>
               <div v-for="task in taskStore.favs" :key="task.id">
                <TaskList :task='task'/>
              </div>
        </div>
  
      
    </main>
  </div>
</template>