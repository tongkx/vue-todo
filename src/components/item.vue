<template>
    <div>
        <div :class="todo.completed ? 'completed' : ''" class="item"><input type="checkbox" v-model="todo.completed"><label>{{todo.content}}</label> <button class="destory" @click = "deleteTodo">删除</button></div>
    </div>
</template>

<script>
  export default {
    name: 'item.vue',
    props: ['todo'],
    data(){
      return {
      }
    },
    methods: {
      deleteTodo(){
        this.$emit('delete',this.todo.id)
      }
    }
  }
</script>

<style lang="scss" scoped type="text/css">
  .completed{
    text-decoration: line-through;
    cursor: pointer;
  }
  .item{
    margin-top: 10px;
  }
</style>
