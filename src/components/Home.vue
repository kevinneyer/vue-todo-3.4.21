<template>
  <div>
    <div>
      <h1>My Todos</h1>
      <!-- <button @click='makeDate'>Date</button> -->
      <div v-if="date">
        {{ date }}
      </div>
      <button class= 'button' @click='formHandler'>{{ form ? 'Hide Form' : 'Create Todo' }}</button>
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
import moment from "moment";

export default {
  name: 'Home',
  components: {
    ToDos,
    CreateForm
  },
  data: function (){
    return {
      todos: [],
      form: false,
      date: ''
    }
  },
  methods: {
    getTodos(){
      fetch('http://localhost:3000/todos')
      .then(res => res.json())
      .then(data => {
        this.todos = data
      })
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
      let toChange = this.todos.find(todo => todo.id === id)
      fetch(`http://localhost:3000/todos/${id}`, {
        method: 'PATCH',
        headers: {
          'Content-Type': 'application/json',
          'Accepts': 'application/json'
        },
        body: JSON.stringify({
          ...toChange,completed: !toChange.completed
        })
      })
      .then(res => res.json())
      .then(data => {
        let newTodos = this.todos.map( todo => {
          if(todo.id === id){
            return { ...todo, completed: data.completed}
          } else
          return todo 
        })
        this.todos = newTodos
      })
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
    },
    makeDate(){
      let date = new Date('2021/04/02')
      this.date = moment(date).format("MMM 'YY").toUpperCase()
      // return this.date
    }
  },
   mounted(){
    this.getTodos()
    this.makeDate()
  }
}
</script>

<style scoped>
  .button{
    background-color: grey;
    color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
}
</style>