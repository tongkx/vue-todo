<template>
  <div class="app">
    <input type="text" class="input-text" v-model="inputValue" placeholder="接下来做什么" @keyup.enter="addTodo">
    <item v-for="todo in filterTodos" :key="todo.id" :todo=todo  @delete=deleteItem></item>
    <tab :filter="filter" :todos = todos @toggle = "toggle" @ClearAllCompleted = "ClearAllCompleted"></tab>
  </div>
</template>

<script>
  import Item from "@/components/item"
  import Tab from "@/components/tabs"
  var id = 1;
export default {
  name: 'App',
  components: {
    item: Item,
    tab: Tab
  },
  data () {
    return {
      inputValue: '',
      todos: [],
      filter: 'all'
    }
  },
  methods: {
    addTodo: function () {
      if (this.inputValue != '') {
        this.todos.unshift({
          id: id++,
          content: this.inputValue,
          completed: false
        });
      }
      this.inputValue = ''
    },
    deleteItem: function (id) {
      this.todos.splice(this.todos.findIndex(todo => todo.id === id), 1)
    },
    toggle (state) {
      this.filter = state
    },
    ClearAllCompleted(){
      this.todos = this.todos.filter(todo => todo.completed)
    }
  },
  computed: {
    filterTodos () {
      if (this.filter === 'all') {
        return this.todos
      }
      const complete = this.filter === 'completed';
      return this.todos.filter(todo => todo.completed === complete)
    }
  }
}
</script>

<style lang="scss" type="text/css">
*{
  margin: 0;
  padding: 0;
}
  ul{
    list-style: none;
  }
  .input-text{
    padding: 5px 8px;
  }
  .app{
    padding: 50px;
  }

</style>
