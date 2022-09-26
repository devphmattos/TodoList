<template>
  <div class="container">

    <h2 class="title">Todo App</h2>

    <form>
      <input placeholder="Enter task" v-model="taskInput" />
      <button type="submit.prevent" @click="addTask">SUBMIT</button>
    </form>

    <table class="table table-bordered">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col">Status</th>
          <th scope="col">Change</th>
          <th scope="col">Delete</th>
        </tr>
      </thead>
      <tbody v-for="(task, index) in tasks" :key="index">
        <tr>
          <td>{{task.name}}</td>
          <div @click="updateTask(index)">
            <td id="btn" style="width: 6rem">{{task.status}}</td>
          </div>
          <td>
            <div class="text-center" @click="editTask(index)">
              <span id="btn" class="fa fa-pen"></span>
            </div>
          </td>
          <td>
            <div class="text-center" @click="deleteTask(index)">
              <span id="btn" class="fa fa-trash"></span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>

  </div>
</template>

<script>
export default {
  data(){
    return{
      tasks: [
        {
          name: 'Ler livro',
          status: 'to-do'
        },
        {
          name: 'Beber 2L água',
          status: 'to-do'
        }
      ],

      taskInput: '',
      editName: '',
      editedTask: null,
      stats: ['to-do', 'in-progress', 'finished'],
      isActive: false
    }
  },

  methods: {
    addTask(){
      if(this.taskInput.length === 0) return

      if(this.editedTask === null){
        this.tasks.push({
          name: this.taskInput,
          status: 'to-do'
        })
        this.taskInput = ''
      }else{
        this.tasks[this.editedTask].name = this.taskInput
        this.taskInput = ''
      }

    },

    deleteTask(index){
      this.tasks.splice(index, 1)
    },

    editTask(index){
      this.taskInput = this.tasks[index].name
      this.editedTask = index
    },

    updateTask(index){
      let newIndex = this.stats.indexOf(this.tasks[index].status);
      if(++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.stats[newIndex];
      

    }

  }
}
</script>

<style scoped>
  .container{
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .title{
    margin: 2rem 0;
  }

  form{
    margin-bottom: 2rem;
  }

  input{
    width: 20rem;
  }

  button{
    background: #6ee7b7;
    transition: 0.2s;
    
  }

  button:hover{
    background: #34d399;
  }

  #btn{
    cursor: pointer;
  }

  .isActive{
    text-decoration: line-through;
  }

</style>
