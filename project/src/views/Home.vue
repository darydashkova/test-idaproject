<template>
    <div class="home">
       <homePageTitle></homePageTitle>
    </div>
</template>
<script>
import homePageTitle from '../components/homePage/homePageTitle.vue'
export default {
    components:{homePageTitle},
    setup() {
        
    },
}
</script>
<style lang="scss">
.home{
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
         background: linear-gradient(blue, pink);
}
</style>