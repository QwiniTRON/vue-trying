<template>
    <form @submit.prevent="onSubmit">
        <input type="text" placeholder="put todo..." v-model="title">
        <button type="submit">Create</button>
        <button type="reset">r</button>
    </form>
</template>
    
<script>
export default {
    methods: {
        onSubmit() {
            let value = this.title.trim()
            if(value.length > 3){
                const newTodo = {
                    id: Date.now(),
                    title: value,
                    compleated: false
                }
                this.$emit('add-todo', newTodo)
                this.title = ''
            }
        }
    },
    data() {
        return {
            title: ''
        }
    }
}
</script>

<style scoped>
form{
    display: flex;
    margin-bottom: 5px;
}

input{
    flex: 1 1 auto;
    border: 1px solid #333;
    background-color: #aaa;
    color: #333;
}

input::placeholder{
    color: #444;
}

button{
    color: #343434;
    background-color: #5f5;
    border: 2px solid #333;
    margin-left: -1px;
    font-weight: 900;
    font-family: 'Courier New', Courier, monospace;
    font-size: 18px;
    text-transform: uppercase;
}
</style>