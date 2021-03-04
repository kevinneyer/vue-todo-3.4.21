<template>
    <div>
        <form class='form'>
            <label>Enter Todo</label><br />
            <textarea v-model="content" type='text' placeholder="Enter todo...."/><br />
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
    }
}
</script>

<style scoped>
    .form{
        display: block;
    }
</style>