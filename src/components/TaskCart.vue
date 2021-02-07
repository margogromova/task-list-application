<template>
  <div class="task-cart my-style">
    <div>
      <h4>{{ model.title }}</h4>
      <p>{{ model.description }}</p>
    </div>
    <div>
      <button @click="emitOnDone" v-if="!model.status" class="btn btn-done">done</button>
      <button @click="emitOnRemove" v-else class="btn btn-remove">remove</button>
    </div>
  </div>
</template>

<script>

export default {
  name: "TaskCart",
  emits: ['onDone', 'onRemove'],
  props: {
    model: {
      required: true,
      default: {
        id: 0,
        title: 'Create video on Youtube',
        description: 'And upload on Youtube',
        status: false
      }
    }
  },
  setup(props, {emit}) {
    const emitOnDone = () => {
      emit('onDone')
    }

    const emitOnRemove = () => {
      emit('OnRemove')
    }

    return {
      emitOnDone,
      emitOnRemove
    }
  }
}
</script>

<style>

.task-cart {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

button, input, .my-style {
  border-radius: 5px;
  border: 1px solid lightgray;
  padding: 10px;
}

.btn {
  cursor: pointer;
  color: white;
}

.btn-done {
  background-color: #2ca92c;

}

.btn-remove {
  background-color: #8d0303;
}

</style>