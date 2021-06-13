<template>
    <div class="wrap">
        <NuxtLink to="/add" class="add">+</NuxtLink>
    </div>
</template>

+
<style lang="scss" scoped>
    .wrap {
        position: absolute;
        right: 0;
        bottom: 0;
        .add {
            position: fixed;
            bottom: 5%;
            width: 50px;
            height: 50px;
            border-radius: 100%;
            background-color: #5181b8;
            text-align: center;
            font-weight: bold;
            font-size: 30px;
            color: #fff;
            margin-left: -51px;
            text-decoration: none;
        }
    }
</style>