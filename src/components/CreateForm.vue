<template>
    <div>
        <form v-on:submit.prevent='submitHandler' class='form'>
            <label>Enter Todo</label><br />
            <input v-model="content" type='text' name='content' placeholder="Enter todo...."/><br />
            <input type='hidden' />
            <input type='submit' />
        </form>
    </div>
</template>

<script>
export default {
    name: 'CreateForm',
    data: function(){
        return{
            content: ''
        }
    },
    methods: {
        submitHandler(){
            let newToDo = {
                content: this.content,
                completed: false
            }
            this.content = ''
            
            this.$emit('submit-handler', newToDo)      
        }
    }
}
</script>

<style scoped>
    .form{
        display: block;
    }
</style>