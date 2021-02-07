<template>
  <main>
    <task-input @onAddTask="addTask"/>
    <ul class="my-list task-list">
      <li v-for="item in taskList" :key="item.id">
        <task-cart @onDemove="removeTask(item.id)" @onDone="setDoneTask(item.id)" :model="item"/>
      </li>
    </ul>
  </main>
</template>

<script>

import TaskCart from "@/components/TaskCart";
import TaskInput from "@/components/TaskInput";
import {ref} from 'vue'

export default {
  name: 'App',
  components: {
    TaskInput,
    TaskCart
  },
  setup() {
    const taskList = ref([{id: 0, title: 'Create video', description: 'And upload on YT', status: false}])

    const addTask = ({title, description}) => {
      taskList.value = [...taskList.value, {
        id: taskList.value[taskList.value.length - 1].id + 1,
        title,
        description,
        status: false
      }]
    }

//где x - текущий єлемент
    const setDoneTask = (id) => {
      taskList.value = taskList.value.map(x => {
        if (x.id === id)
          x.status = true
        return x
      })
    }

    const removeTask = (id) => {
      taskList.value = taskList.value.filter(x => x.id !== id)

    }
    return {
      taskList,
      addTask,
      removeTask,
      setDoneTask
    }
  }
}
</script>

<style>
* {
  font-family: "JetBrains Mono", monospace;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 0;
  padding: 0;
}

main {
  max-width: 450px;
  margin: 0 auto;
}

.task-list {
  list-style: none;
}
</style>
