<template>
  <li>
    <span :class="{done: todo.completed}">
      <input type="checkbox" v-model="todo.completed">
      <strong>{{index + 1}}</strong>
      {{todo.title | uppercase}}
    </span>
    <button class="rm" 
      @click="$emit('remove-todo', todo.id)"
    >&times;</button>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    },
    index: Number
  },  
  filters: {
    uppercase(value) {
      return value.toUpperCase()
    }
  }
}
</script>

<style scoped>
  li {
    border: 1px solid #ccc;
    display: flex;
    justify-content: space-between;
    padding: .5rem 2rem;
    margin-bottom: 1rem;    
  }

  input {
    margin-right: 1rem;
  }

  .rm {
    background: red;
    color: #fff;
    border-radius: 50%;
    border-width: 0px;
    font-weight: bold;
  }

  .done {
    text-decoration: line-through;
  }
</style>
