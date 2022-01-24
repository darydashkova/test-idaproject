<template>
    <div class="catalog-products">
            <div class="catalog-products__card" v-for="(product, index) in data" :key="index" >
                 <div class="catalog-products__card-img" :style="{ backgroundImage: `url('${product.img}')` }"></div>
                 <div class="catalog-products__card-title"> {{product.name}}</div>
                 <div class="catalog-products__card-text">{{product.text}}</div>
                 <div class="catalog-products__card-price">{{formattedPrice(product.price)}} руб.</div>
               
        </div>

    </div>
</template>
<script>
import {ref} from 'vue'
export default {
    props:{
        data:Object,
        },
    setup(props) {
        const price = ref('')
         const formattedPrice = (item) => {
             
            item = item.replace(/\s/g, '');
            const copyPrice = ref()
            copyPrice.value=String(item)
            copyPrice.value =  item.replace(/(\d)(?=(\d{3})+([^\d]|$))/g, "$1 ")
            price.value=copyPrice.value
            return price.value
        }
        return{
            formattedPrice,
        }
    },
}
</script>
<style lang="scss">
.catalog-products{
    display: flex;
    flex-wrap: wrap;
    width: 100%;
    margin-left: 332px;
    &__card{
        width: 100%;
        max-width: 332px;
        min-width: 250px;
        background: #FFFEFB;
        box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
        border-radius: 4px;
        margin-left: 16px;
        margin-bottom: 16px;
        border-radius: 4px;
        overflow: hidden;
        &-img{
            width: 332px;
            height: 200px;
            background-repeat: no-repeat;
            background-size: cover;
        }
        &-title{
            padding: 16px ;
            font-style: normal;
            font-weight: 600;
            font-size: 20px;
            line-height: 25px;
            color: #3F3F3F;
            text-align: left;  
        }
        &-text{
            padding: 0px 16px 32px;
            text-align: left;
            font-size: 16px;
            line-height: 20px;
            color: #3F3F3F;
        }
        &-price{
            padding: 0px 16px 24px;
            text-align: left;
            font-weight: 600;
            font-size: 24px;
            line-height: 30px;
            color: #3F3F3F;
        }
    }
}
</style>