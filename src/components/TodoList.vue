<template>
  <TodoForm v-if="editData.id" :editData="editData" @submit="updateTodo" />
  <div class="todo-list" v-else>
    <div :class="['todo-row', {'complete': todo.isCompleted}]"
         v-for="(todo, index) in todos"
         :key="index">

      <div @click="completeTodo(todo.id)">
        {{ todo.text }}
      </div>

      <div class="icons">
        <TrashIcon class="delete-icon" @click="deleteTodo(todo.id)" />
        <PencilIcon class="edit-icon" @click="editTodo(todo)" />
      </div>
    </div>
  </div>
</template>

<script>
import TodoForm from './TodoForm'
import { TrashIcon, PencilIcon } from '@vue-hero-icons/outline'

export default {
  name: 'TodoList',
  props: {
    todos: {
      type: Array,
      default: () => ([])
    }
  },
  components: {
    TodoForm,
    TrashIcon,
    PencilIcon
  },
  data () {
    return {
      editData: {
        id: null,
        text: ''
      }
    }
  },
  created () {
    console.log(this.todos)
  },
  methods: {
    completeTodo (todoId) {
      this.$emit('completeTodo', todoId)
    },
    deleteTodo (todoId) {
      this.$emit('deleteTodo', todoId)
    },
    updateTodo (todo) {
      this.$emit('submitUpdate', this.editData.id, todo)
      this.editData = {
        id: null,
        text: ''
      }
    },
    editTodo (todo) {
      this.editData = { ...todo }
    }
  }
}
</script>
