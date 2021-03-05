<template>
    <div class='form-container'>
        <form v-on:submit.prevent='submitHandler' class='form'>
            <input class='text' v-model="content" type='text' name='content' placeholder="Enter todo...."/><br />
            <input type='hidden' />
            <input class='button' type='submit' />
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
        margin-top: .25em;
        margin-bottom: .25em;
        display: block;
    }
    .form-container{
        /* border-style: dashed;
        border-color: black; */
        width: 25%;
        margin-right: auto;
        margin-left: auto;
    }
    .text{
        width: 75%;
        height: 40px;
        margin-right: auto;
        margin-left: auto;
        margin-top: 1em;
        margin-bottom: 1em;
    }

    .button{
        background-color: black;
        color: white;
        /* margin-top: .25em; */
        margin-bottom: .25em;
          padding: 15px 32px;
        text-align: center;
        text-decoration: none;
        display: inline-block;
        font-size: 16px;
    }
</style>