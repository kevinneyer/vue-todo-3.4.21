<template>
  <div>
    <ToDos :todos="todos" />
  </div>
</template>

<script>
import ToDos from './ToDos'

export default {
  name: 'Home',
  components: {
    ToDos
  },
  data: function (){
    return {
      todos: []
    }
  },
  methods: {
    async getTodos(){
      let results = await fetch('http://localhost:3000/todos')
      let data = await results.json()
      return data
    }
  },
  async mounted(){
    this.todos = await this.getTodos()
  
  }
  
}
</script>