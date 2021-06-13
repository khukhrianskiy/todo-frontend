<template>
    <div class="block">
        <div>Add new Todo item</div>
        <form action="" v-on:submit.prevent="submit">
            <div>
                <input type="text" placeholder="Todo Text" v-model="todoItem.text">
            </div>
            <div>
                <input type="text" placeholder="Add hashtags" v-model="todoItem.hashtags">
            </div>
            <div>
                <input type="text" placeholder="Add category" v-model="todoItem.categories">
            </div>
            <div>
                <input type="text" placeholder="Add end date" v-model="todoItem.endDate">
            </div>
            <div>
                <input type="submit" value="Save">
            </div>
        </form>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    props: [
        'id',
    ],
    data: function () {
        return {
            todoItem: {
                text: null,
                hashtags: null,
                categories: null,
                endDate: null,
            }
        }
    },
    mounted() {
        if (this.id) {
            axios.get(`http://localhost/api/todo-items/${this.id}`)
                .then(response => {
                    this.todoItem = response.data;
                })
                .catch(error => {})
        }
    },
    methods: {
        submit: function () {
            axios.post('http://localhost/api/todo-items',
                {
                    text: this.todoItem.text,
                    hashtags: this.todoItem.hashtags.split(','),
                    categories: this.todoItem.categories.split(','),
                    endDate: this.todoItem.endDate
                },
                {headers: {'Accept': 'application/json'}}
            )
            .then(response => {
                if (response.status === 201) {
                    this.created();
                }
            })
            .catch(error => {})
        },
        created: function () {
            this.todoItem.text = '';
            this.todoItem.hashtags = '';
            this.todoItem.categories = '';
            this.todoItem.endDate = '';
        }
    }
}
</script>

<style>
.block {
    width: 400px;
    margin: 0 auto;
}
</style>