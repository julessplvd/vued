<template>
  <div class='ui centered card'>

    <div class="content" v-show="!isEditing">
      <div class='header'>
          {{ todo.title }}
      </div>
      <div class='meta'>
          {{ todo.project }}
      </div>
      <div class='extra content todo-action-buttons'>
        <span class='right floated edit icon' v-on:click="showForm">
          <i class='edit icon'></i>
        </span>
        <span class='right floated trash icon' v-on:click="deleteTodo(todo)">
          <i class='trash red icon'></i>
        </span>
      </div>
    </div>

    <div class="content" v-show="isEditing">
      <div class='ui form'>
        <div class='field'>
          <label>Title</label>
          <input type='text' v-model="todo.title" >
        </div>
        <div class='field'>
          <label>Description</label>
          <input type='text' v-model="todo.project" >
        </div>
        <button class='ui primary button' v-on:click="hideForm">
          Save
        </button>
      </div>
    </div>

    <div v-on:click="completeTodo(todo)" :class="classStatusColor" class='ui bottom attached button' v-show="!isEditing">
        {{ statusText }}
    </div>
  </div>
</template>

<script type="text/javascript">
export default {
  props: ['todo'],
  data() {
    return {
      isEditing: false,
    };
  },
  methods: {
    showForm() {
      this.isEditing = true;
    },
    hideForm() {
      this.isEditing = false;
    },
    deleteTodo(todo) {
      this.$emit('delete-todo', todo);
    },
    completeTodo(todo) {
      this.$emit('complete-todo', todo);
    },
  },
  computed: {
    statusText() {
      return this.todo.done ? 'Completed' : 'Pending'
    },
    classStatusColor() {
      return this.todo.done ? 'green' : ''
    },
  }
};
</script>