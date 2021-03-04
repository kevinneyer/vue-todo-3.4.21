<template>
    <div>
        <div v-for='todo in todos' :key="todo.id">
            <ToDo :todo="todo"/>
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