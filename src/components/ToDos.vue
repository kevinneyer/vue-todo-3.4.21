<template>
    <div>
        <div v-for='todo in todos' :key="todo.id">
            <ToDo 
            @complete-handler="$emit('complete-handler', todo.id)" 
            @delete-handler="$emit('delete-handler', todo.id)"
            :todo="todo"/>
        </div>
    </div>
</template>

<script>

import ToDo from './ToDo'

export default {
  name: 'ToDos',
  props: ['todos'],
  components: {
      ToDo
  }
}
</script>