<template>
    <div>
        <h1>My Todos</h1>
        <ToDo :todos="todos"/>
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