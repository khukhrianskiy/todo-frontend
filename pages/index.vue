<template>
    <div class="wrap">
        <TodoItem v-for="todoItem in todoItems" v-bind:todoItem="todoItem"/>
        <ButtonAdd/>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data: function () {
        return {
            todoItems: [],
        }
    },
    mounted() {
        axios.get('http://localhost/api/todo-items')
            .then(response => {
                this.todoItems = response.data;
            })
            .catch(error => {})
    },
}
</script>

<style lang="scss">
    .wrap {
        position: relative;
        width: 100%;
    }
</style>
