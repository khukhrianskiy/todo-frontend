<template>
    <div class="block todo-item">
        <div class="actions">
            <div class="menu" v-on:click="isHidden = !isHidden">
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
            </div>
            <div class="dropdown" v-if="!isHidden">
                <NuxtLink :to="`/edit?id=${todoItem.id}`">Edit</NuxtLink>
                <div class="delete" v-on:click="remove(todoItem.id)">Delete</div>
            </div>
        </div>
        <div class="text">{{ todoItem.text }}</div>
        <div class="hashtags">
            <a :href="`#${hashtag.name}`" v-for="hashtag in todoItem.hashtags">#{{ hashtag.name }}</a>
        </div>
        <div class="category">
            <a :href="`${category.name}`" v-for="category in todoItem.categories">{{ category.name }}</a>
        </div>
        <div class="end-date">{{ todoItem.end_date }}</div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    props: ['todoItem'],
    data: () => ({
        isHidden: true,
    }),
    methods: {
        remove: function (id) {
            axios.delete(`http://localhost/api/todo-items/${id}`)
                .then(() => {
                    this.$delete;
                })
                .catch(error => {})
        }
    }
}
</script>

<style lang="scss" scoped>
.todo-item {
    display: flex;
    align-items: center;
    width: 100%;
    margin-bottom: 20px;
}
.actions {
    margin-right: 10px;
    position: relative;
    .menu {
        cursor: pointer;
        width: 20px;
    }
    .icon-bar {
        display: block;
        background-color: #666;
        width: 4px;
        height: 4px;
        border-radius: 2px;
        margin-left: 3px;
        margin-right: 3px;

        + .icon-bar {
            margin-top: 2px;
        }
    }
    .dropdown {
        position: absolute;
        background-color: #ffffff;
        border: 1px solid #ccc;
        padding: 5px 15px;
        min-width: 100px;
        top: 30px;
        left: -14px;
        z-index: 50;
        box-shadow: 0 3px 4px #666;
        &:before {
            content: "";
            position: absolute;
            border: 10px solid transparent;
            border-bottom-color: #ccc;
            top: -21px;
            left: 8px;
        }
        &:after {
            content: "";
            position: absolute;
            border: 10px solid transparent;
            border-bottom-color: #fff;
            top: -19px;
            left: 8px;
        }
        .delete {
            cursor: pointer;
        }
    }
}
.text {
    margin-right: 10px;
    font-weight: bold;
    white-space: nowrap;
    overflow-x: hidden;
    text-overflow: ellipsis;
    width: 40%;
}
.hashtags {
    margin-right: 10px;
    min-width: 20%;
    a {
        color: #666;
        text-decoration: none;
        margin-right: 5px;
    }
}
.end-date {
    margin-left: auto;
    width: 10%;
}
</style>
