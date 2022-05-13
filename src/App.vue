<template>
  <div>
    <input type="text" v-model="task">
    <button @click="addTask">Add</button>
    <br>
    <br>
    <div>
      <ul>
        <li v-for="(taskObj, index) in taskList" :key="taskObj">
          <span :class="{completedTask: taskObj.completed}">{{ taskObj.task }}</span> &nbsp;
          <button @click="editTask(index)">Edit</button>
          <button @click="deleteTask(index)">Delete</button>
          <button @click="completedTask(index)">Completed</button>
          <button @click="resetTask(index)">Reset</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data(){
    return{
      taskList: [],
      task: '',
      index: null,
    };
  },
  methods: {
    addTask(){
      if(this.index != null){
        this.taskList[this.index].task = this.task;
        this.task = '';
        this.index = null;
      }
      else{
        this.taskList.push({
          task: this.task,
          completed: false,
        });
        this.task = '';
      }
    },
    deleteTask(index){
      this.taskList.splice(index, 1);
    },
    editTask(index){
      this.task = this.taskList[index].task;
      this.index = index;
    },
    completedTask(index){
      this.taskList[index].completed = true;
    },
    resetTask(index){
      this.taskList[index].completed = false;
    },
  },
}
</script>

<style>
.completedTask{
  text-decoration: line-through;
}
</style>
