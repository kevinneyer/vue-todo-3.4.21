<template>
  <div>
    <div>
      <h1>My Todos</h1>
      <button @click='formHandler'>{{ form ? 'Hide Form' : 'Create Todo' }}</button>
    </div>
    <div v-if='form'>
      <CreateForm @submit-handler='addHandler'/>
    </div>
    <ToDos 
    @complete-handler='completeHandler' 
    @delete-handler='deleteHandler'
    :todos="todos" />
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
    },
    addHandler(todo){
      fetch('http://localhost:3000/todos', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
          'Accepts': 'application/json'
        },
        body: JSON.stringify(todo)
      })
      .then(res => res.json())
      .then(data => {
        this.todos = [...this.todos, data]
      })
    },
    completeHandler(id){ // does not persist
        let todo = this.todos.filter( todo => todo.id === id)
        fetch(`http://localhost:3000/todos/${id}`, {
         method: 'PUT',
         headers: {
           'Content-Type': 'application/json',
           'Accepts': 'application/json'
         },
         body: JSON.stringify({ ...todo, completed: !todo.completed})
       })
       .then(res => res.json())
       .then(data => 
       console.log(data)
          // this.todos = this.todos.map( todo => {
          //   if(todo.id === id){
          //     return { ...todo, completed: data.completed}
          //   } else
          //   return todo 
          // })
       )
    },
    deleteHandler(id){
       fetch(`http://localhost:3000/todos/${id}`, {
         method: 'DELETE',
         headers: {
           'Content-Type': 'application/json'
         }
       })
       .then(() => {
          this.todos = this.todos.filter( todo => todo.id !== id)
       })
    }
  },
  async mounted(){
    this.todos = await this.getTodos()
  }
}
</script>