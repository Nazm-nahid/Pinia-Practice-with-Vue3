  <template>
    <main>
      <header>
        <img src=".\assets\image.png" alt="pinia logo">
        <h1>Pinia Task</h1>
      </header>
      
      <div class="new-task-form">
        <TaskForm/>
      </div>
      <nav class="filter">
        <button @click="filter='favs'">Favorite</button>
        <button @click="filter='all'">Show All</button>
      </nav>

      <div class="loading" v-if="taskStore.loading">Loading...</div>
      
      <div class="task-list" v-if="filter === 'all'">
        <p>You have {{ taskStore.totalCount }} task to do</p>
        <div v-for="task in taskStore.tasks"> 
          <TaskDetails :task="task"/>
        </div>
      </div>

      <div class="task-list" v-if="filter === 'favs'">
        <p>You have {{ taskStore.favCount }} favorite task to do</p>
        <div v-for="task in taskStore.favs"> 
          <TaskDetails :task="task"/>
        </div>
      </div>

    </main>
  </template>
  
  <script>
  import { ref} from 'vue';
  import TaskDetails from './components/TaskDetails.vue'
  import TaskForm from './components/TaskForm.vue'
  import { useTaskStore } from './stores/TaskStore';

    export default {
      components: { TaskDetails , TaskForm },
      setup () {
        const taskStore = useTaskStore()

        taskStore.getTasks()
        
        const filter = ref('all')

        return { taskStore, filter }
      }
    }
  </script>