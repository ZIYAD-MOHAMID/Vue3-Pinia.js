<script setup>
import { defineProps } from "vue";
import { useTaskStore } from "../stores/taskStor";
const { task } = defineProps(["task"]);
const taskStor = useTaskStore();
</script>

<template>
  <main>
    <div class="task">
      <h3>{{ task.title }}</h3>
      <div class="icons">
        <i class="fab fa-500px" @click="taskStor.deleteTask(task.id)">
          delete</i
        >
        <i
          class="fab fa-500px"
          @click="taskStor.toggleFav(task.id)"
          :class="{ active: task.isFav }"
        >
          favorite</i
        >
      </div>
    </div>
  </main>
</template>

<style scoped lang="scss">
.task {
  padding: 6px 20px;
  background-color: #fff;
  margin-top: 20px;
  border-radius: 4px;
  box-shadow: 2px 4px 6px #0000005d;
  display: flex;
  justify-content: space-between;
  align-items: center;
  i.active {
    color: #ff005d;
  }
  h3,
  .icons {
    display: inline-block;
  }
  .icons {
    text-align: right;
  }
  i {
    font-size: 1.4em;
    margin-left: 6px;
    cursor: pointer;
    color: #bbb;
  }
}
</style>
