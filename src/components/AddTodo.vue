<template>
  <div class="w-100 text-end">
    <button
      type="submit"
      class="btn btn-success my-2"
      data-bs-toggle="modal"
      data-bs-target="#addTodoModal"
    >
      Add new task
    </button>
  </div>

  <!-- addTodomodal -->

  <div
    class="modal fade"
    id="addTodoModal"
    tabindex="-1"
    aria-labelledby="exampleModalLabel"
    aria-hidden="true"
  >
    <div class="modal-dialog modal-dialog-centered">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Add new task</h5>
          <button
            type="button"
            class="btn-close"
            data-bs-dismiss="modal"
            aria-label="Close"
          ></button>
        </div>
        <div class="modal-body">
          <input
            class="w-100"
            type="text"
            placeholder="do something....."
            v-model="title"
          />
        </div>
        <div class="modal-footer">
          <button
            type="button"
            class="btn btn-secondary"
            data-bs-dismiss="modal"
          >
            Close
          </button>
          <button
            type="button"
            class="btn btn-success"
            data-bs-dismiss="modal"
            v-on:click="addTodo"
          >
            Add
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import { v4 as uuidv4 } from 'uuid';

export default {
  name: 'AddTodo',
  setup(props, context) {
    const title = ref('');

    const addTodo = (e) => {
      e.preventDefault();

      const newTodo = {
        id: uuidv4(),
        title: title.value,
        completed: false,
      };

      context.emit('add-todo', newTodo);
      title.value = '';
    };

    return {
      title,
      addTodo,
    };
  },
};
</script>

<style>
.addBtn {
  background-color: green;
  color: white;
  border: none;
  cursor: pointer;
  padding: 0.5rem;
  border-radius: 10px;
}
</style>
