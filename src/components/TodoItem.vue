<template>
  <div
    :class="['todoItem my-2', todoProps.completed ? 'isComplete' : '']"
    id=""
  >
    <span class="d-flex align-items-center">
      <input
        type="checkbox"
        v-bind:checked="todoProps.completed"
        v-on:change="markItemCompleted"
        v-bind:id="todoProps.id"
      />
      <label :for="todoProps.id">{{ todoProps.title }}</label>
    </span>
    <button class="btn btn-danger" v-on:click="deleteItem">Delete</button>
  </div>
</template>

<script>
export default {
  name: 'TodoItem',
  props: ['todoProps'],
  setup(props, context) {
    const markItemCompleted = () => {
      console.log(props.todoProps);
      context.emit('item-completed', props.todoProps.id);
    };

    const deleteItem = () => {
      context.emit('item-delete', props.todoProps.id);
    };

    return {
      markItemCompleted,
      deleteItem,
    };
  },
};
</script>

<style>
.todoItem {
  border: 1px solid #ccc;
  padding: 0.7rem;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.isComplete span {
  text-decoration: line-through;
}

.todoItem input {
  height: 1rem;
  width: 2rem;
}
</style>
