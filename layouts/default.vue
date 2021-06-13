<template>
    <div>
        <header>
            <div class="container">
                <HeaderLogo/>
                <HeaderProfile/>
            </div>
        </header>
        <div class="container">
            <Nuxt/>
        </div>
        <footer></footer>
    </div>
</template>

<style lang="scss">
header {
    background-color: #5181b8;
    height: 60px;
    margin-bottom: 20px;

    .container {
        display: flex;
        align-items: center;
        height: 100%;
    }
}
</style>
