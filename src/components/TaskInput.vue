<template>
  <div class="my-list task-input">
    <input v-model="title" placeholder="Title" type="text">
    <input v-model="description" placeholder="Description" type="text">
    <button @click="onAddTask">add task</button>

  </div>
</template>

<script>
import {ref} from 'vue'

export default {
  name: "TaskInput",
  emits: {
    onAddTask({title, descroption}) {
      if (title === '' || descroption === '') {
        alert('Fill some info please!!')
        return false
      }
      return true
    }
  },
  // data() {
  //   return {
  //     title: '',
  //     description: ''
  //   }
  // }

  // или

  setup(props, {emit}) {
    const title = ref('')
    const description = ref('')

    const onAddTask = () => {
      emit('onAddTask', {title: title.value, description: description.value})
    }

    return {
      title,
      description,
      onAddTask
    }
  }

}
</script>

<style>
.my-list {
  display: grid;
  grid-template-rows: auto;
  grid-template-columns: 100%;
  grid-gap: 5px;
}

.task-input {
  margin: 10px 0;
}

</style>