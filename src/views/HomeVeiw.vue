<script setup>
import TaskDetailsVue from "../components/TaskDetails.vue";
import taskForm from "../components/taskForm.vue";

import { useTaskStore } from "../stores/taskStor";
import { ref } from "vue";
import { storeToRefs } from "pinia";
let fillter = ref("all");

const taskStor = useTaskStore();

const { tasks, favs, totalCount, favCount } = storeToRefs(taskStor);
</script>

<template>
  <main>
    <header>
      <img src="../assets/imgs/kill.jpg" alt="" />
      <h1>{{ taskStor.name }}</h1>
    </header>

    <div class="new-task-form">
      <taskForm />
    </div>

    <nav class="fillter">
      <button @click="fillter = 'all'">All Tasks</button>
      <button @click="fillter = 'favs'">Fav Tasks</button>
    </nav>

    <div class="task-list" v-if="fillter === 'all'">
      <p>Your have {{ taskStor.totalCount }} tasks left to do</p>
      <div v-for="task in tasks" :key="task.id">
        <TaskDetailsVue :task="task" />
      </div>
    </div>
    <div class="task-list" v-if="fillter === 'favs'">
      <p>Your have {{ taskStor.favCount }} Fav tasks left to do</p>
      <div v-for="task in favs" :key="task.id">
        <TaskDetailsVue :task="task" />
      </div>
    </div>

    <button @click="taskStor.$reset">reset</button>
  </main>
</template>

<style scoped lang="scss">
header {
  text-align: center;
  background-color: #e7e7e7;
  padding: 20px 0 0 0;
  display: flex;
  justify-content: center;
  align-items: center;
  img {
    max-width: 60px;
    transform: rotate(-10deg);
    border-radius: 10%;
  }
  h1 {
    margin: 0;
    font-size: 2em;
    padding-top: 25px;
    margin-left: 15px;
    color: #777;
    transform: rotate(2deg);
  }
}
.new-task-form {
  background: #e7e7e7;
  padding: 20px 0;
}
.fillter {
  width: 640px;
  margin: 10px auto;
  text-align: right;
  button {
    display: inline-block;
    margin-left: 10px;
    background-color: #fff;
    border: 2px solid #555;
    border-radius: 4px;
    padding: 4px 8px;
    cursor: pointer;
    font-size: 1em;
  }
}
.task-list {
  max-width: 640px;
  margin: 20px auto;
}
</style>
