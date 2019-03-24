<template>
  <div>
    <div class="tab-wrap">
      <div class="tab-left">{{unfinlishedCompleteLen}} items left</div>
      <ul class="tab-content">
        <li v-for="state in tabs" :class="filter === state ? 'active' : ''" @click="toggleFilter(state)">{{state}}</li>
      </ul>
      <div class="tab-right" @click="ClearAllCompleted">Clear Completed</div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'tabs',
    props:['filter','todos'],
    data () {
      return {
        tabs: ['all', 'active', 'completed']
      }
    },
    methods:{
      toggleFilter(state){
        this.$emit('toggle',state);

      },
      ClearAllCompleted(){
        this.$emit('ClearAllCompleted')
      }
    },
    computed:{
      unfinlishedCompleteLen(){
        return this.todos.filter(todo => !todo.completed).length;
      }
    }
  }
</script>

<style lang="scss" scoped type="text/css">
  .tab-wrap{
    width: 600px;
    line-height: 36px;
    margin-top: 15px;
    display: flex;
    .tab-content{
      flex:1
    }
  }
  .tab-content {
    li {
      margin-left: 20px;
      float: left;
      &.active {
        padding: 0 12px;
        border: 1px solid #f00;
      }
    }
  }

</style>
