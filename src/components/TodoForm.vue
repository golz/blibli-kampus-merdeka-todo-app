<template>
  <form class="todo-form" @submit.prevent="handleSubmit">
    <input type="text"
           v-model="text"
           :placeholder="placeholderText"
           ref="input"
           class="todo-input">
    <button class="todo-button">{{ actionLabel }}</button>
  </form>
</template>

<script>
export default {
  name: 'TodoForm',
  props: {
    editData: {
      type: Object,
      default: null
    }
  },
  data () {
    return {
      text: this.editData ? this.editData.text : ''
    }
  },
  mounted () {
    this.$refs.input.focus()
  },
  computed: {
    placeholderText () {
      return this.editData ? 'Update your todo' : 'Add your new todo'
    },
    actionLabel () {
      return this.editData ? 'Update' : 'Add new todo'
    }
  },
  methods: {
    handleSubmit () {
      this.$emit('submit', {
        id: Math.floor(Math.random() * 10000),
        text: this.text
      })
      this.resetForms()
    },
    resetForms () {
      this.text = ''
    }
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/variable.scss';

.todo-form {
  margin-bottom: 32px;
}

.todo-input {
  padding: 14px 32px 14px 16px;
  border-radius: 8px 0 0 8px;
  border: 2px solid $blue;
  outline: none;
  width: 320px;
  background: transparent;
  color: $black;
}

.todo-input::placeholder {
  color: #5c5c5c;
}

.todo-button {
  padding: 16px;
  border: none;
  border-radius: 0 8px 8px 0;
  cursor: pointer;
  outline: none;
  background: linear-gradient(
      90deg,
      $blue 0%,
      #0eb3ff 100%
  );
  color: $white;
  text-transform: capitalize;
}

.todo-input.edit {
  border: 2px solid #149fff;
}

.todo-button.edit {
  background: linear-gradient(
      90deg,
      $blue 0%,
      #0eb3ff 100%
  );
  padding: 16px 22px;
}
</style>
