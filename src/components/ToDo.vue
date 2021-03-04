<template>
    <div v-if="todo.completed === false" class='todo-card'>
        <h3>{{ todo.content }}</h3>
        <button>Mark as Complete</button>
    </div>
    <div v-else-if="todo.completed === true" class='disabled'>
        <h3>{{ todo.content }}</h3>
    </div>
</template>

<script>
export default {
    name: 'Todo',
    props: ['todo'],
}
</script>

<style scoped>
    .todo-card{
        margin-top: 1em;
        margin-bottom: 1em;
        border: black;
        border-style: solid;
        width: 50%;
        margin-right: auto;
        margin-left: auto;
    }

    .disabled{
        margin-top: 1em;
        margin-bottom: 1em;
        border: rgb(145, 145, 145);
        border-style: solid;
        width: 50%;
        margin-right: auto;
        margin-left: auto;
        background-color: rgb(145, 145, 145);
        color: rgb(201, 201, 201)
    }
</style>