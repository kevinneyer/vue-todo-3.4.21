<template>
  <div>
    <div>
      <h1>My Todos</h1>
      <button @click='formHandler()'>{{ form ? 'Hide Form' : 'Create Todo' }}</button>
    </div>
    <div v-if='form'>
      <CreateForm />
    </div>
    <ToDos :todos="todos" />
  </div>
</template>

<script>
import ToDos from './ToDos'
import CreateForm from './CreateForm'

export default {
  name: 'Home',
  components: {
    ToDos,
    CreateForm
  },
  data: function (){
    return {
      todos: [],
      form: false
    }
  },
  methods: {
    async getTodos(){
      let results = await fetch('http://localhost:3000/todos')
      let data = await results.json()
      return data
    },
    formHandler(){
      this.form = !this.form
    }
  },
  async mounted(){
    this.todos = await this.getTodos()
  
  }
  
}
</script>