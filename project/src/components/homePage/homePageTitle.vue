<template>
    <div class="home-title">
        <div class="home-title__title">Тестовое задание</div>
        <router-link to="/products" class="home-title__link">Перейти к созданию товаров</router-link>
    </div>
</template>
<style lang="scss">
.home-title{
    width: 100%;
    &__title{
        font-size: 45px;
        margin-bottom: 50px;
    }
    &__link{
        text-decoration: none;
        text-transform: uppercase;
        background-color: blue;
        padding: 10px;
        border-radius: 5px;
        
    }
}
</style>