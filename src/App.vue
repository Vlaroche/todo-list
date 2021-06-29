<template>
  <div id="app" class="h-screen overflow-hidden flex items-center justify-center">
    <div class=" w-full p-8 flex justify-center font-sans">
      <TodoList/>
    </div>
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'

export default {
  name: 'App',
  components: {
    TodoList
  },
}
</script>

<style>
#app {
}
</style>
