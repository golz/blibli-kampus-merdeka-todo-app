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

<style lang="scss" scoped>
@import '@/assets/variable.scss';

.complete {
  text-decoration: line-through;
  opacity: 0.4;
}

.todo-container {
  display: flex;
  flex-direction: row;
  position: relative;
}

.todo-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 4px auto;
  color: $white;
  background: linear-gradient(
      90deg,
      #f7931e 0%,
      #f8a33f 100%
  );

  padding: 16px;
  border-radius: 8px;
  width: 90%;
}

.todo-row:nth-child(4n + 1) {
  background: linear-gradient(
      90deg,
      #8bc63f 0%,
      #9bce59 100%
  );
}

.todo-row:nth-child(4n + 2) {
  background: linear-gradient(
      90deg,
      #ec008c 0%,
      #ff0f9d 100%
  );
}

.todo-row:nth-child(4n + 3) {
  background: linear-gradient(
      90deg,
      $blue 0%,
      #0eb3ff 100%
  );
}

.icons {
  display: flex;
  align-items: center;
  font-size: 24px;
  cursor: pointer;
}

.delete-icon {
  margin-right: 5px;
  color: $white;
}

.edit-icon {
  color: $white;
}
</style>
