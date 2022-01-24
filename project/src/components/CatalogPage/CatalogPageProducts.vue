<template>
    <div class="catalog-products">
            <div class="catalog-products__card" v-for="(product, index) in data" :key="index" >
                <img src="../../assets/delete.svg" class="catalog-products__card-delete" @click="openModal(index)">
              <div class="catalog-products__card_overflow">
                <div class="catalog-products__card_top">
                    <div class="catalog-products__card-img" :style="{ backgroundImage: `url('${product.img}')` }"></div>
                    <div class="catalog-products__card-title"> {{product.name}}</div>
                    <div class="catalog-products__card-text">{{product.text}}</div>
                 </div>
                 <div class="catalog-products__card-price">{{formattedPrice(product.price)}} руб.</div>  
                 </div>
        </div>
    </div>
</template>
<script>
import {ref} from 'vue'


export default {
    props:{
        data:Object,
        },
        emits:['openModal'],
    setup(props, {emit}) {
        const price = ref('')
         const formattedPrice = (item) => {
             
            item = item.replace(/\s/g, '');
            const copyPrice = ref()
            copyPrice.value=String(item)
            copyPrice.value =  item.replace(/(\d)(?=(\d{3})+([^\d]|$))/g, "$1 ")
            price.value=copyPrice.value
            return price.value
        }
        const openModal = (index) => {
            emit('openModal', index)
        }
        return{
            formattedPrice,
            openModal
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
     @media (max-width: 728px) {
       margin-left: inherit;
     }
     @media (max-width: 768px) {
       margin-left: -50px;
       justify-content: center;
       margin-top: 470px;
    }
    &__card{
        position: relative;
        width: 100%;
        max-width: 332px;
        min-width: 250px;
        background: #FFFEFB;
        box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
        border-radius: 4px;
        margin-left: 16px;
        margin-bottom: 16px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;

         @media (max-width: 728px) {
            margin-left: 0;
        }
         @media (max-width: 768px) {
            margin-left: 50px;
        }
        &_overflow{
            border-radius: 4px;
            overflow: hidden;
            height: 100%;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }
        &-delete{
            display: none;
            height: 0;
            }
        &:hover{
            .catalog-products__card-delete{
                display: inherit !important;
                height: auto !important;
                z-index: 999;
                position: absolute;
                right: 0;
                cursor: pointer;
                right: -15px;
                top: -15px;
            }
        }
        &-img{
            width: 332px;
            height: 200px;
            background-repeat: no-repeat;
            background-size: cover;
            @media (max-width: 768px) {
                width: 100%;
                height: 180px;
            }
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