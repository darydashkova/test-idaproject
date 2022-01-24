<template>
    <div class="catalog-form">
        <div class="catalog-form__item">
            <div class="catalog-form__item-title">Наименование товара
                <svg width="4" height="4" viewBox="0 0 4 4" fill="none" xmlns="http://www.w3.org/2000/svg">
                <rect width="4" height="4" rx="2" fill="#FF8484"/>
                </svg>
            </div>
            <input class="catalog-form__item-input" placeholder="Введите наименование товара" v-model="name" :class="{'error' : error.name}">
        </div>
        <div class="catalog-form__item">
            <div class="catalog-form__item-title">Описание товара</div>
            <textarea class="catalog-form__item-textarea" placeholder="Введите описание товара" v-model="text" ></textarea>
        </div>
        <div class="catalog-form__item">
            <div class="catalog-form__item-title">Ссылка на изображение товара
                <svg width="4" height="4" viewBox="0 0 4 4" fill="none" xmlns="http://www.w3.org/2000/svg">
                <rect width="4" height="4" rx="2" fill="#FF8484"/>
                </svg>
            </div>
            <input class="catalog-form__item-input" placeholder="Введите ссылку" v-model="img" :class="{'error' : error.img}">
        </div>
        <div class="catalog-form__item">
            <div class="catalog-form__item-title">Цена товара
                <svg width="4" height="4" viewBox="0 0 4 4" fill="none" xmlns="http://www.w3.org/2000/svg">
                <rect width="4" height="4" rx="2" fill="#FF8484"/>
                </svg>
            </div>
            <input class="catalog-form__item-input" placeholder="Введите цену"  @input="thouthands(price)" v-model="price" :class="{'error' : error.price}">
        </div>
        <div class="catalog-form__item">
            <div class="catalog-form__item-button inter" @click="add">Добавить товар</div>
        </div>
    </div>
</template>
<script>

import {ref} from 'vue'

export default {
    setup() {
        const price = ref('')
        const name = ref('')
        const img = ref('')
        const text = ref('')
        const formattedPrice = (form) => {
            const value = ref(form); 
            var rep = /[-":'a-zA-Zа-яА-Я]/; 
            if (rep.test(value.value)) { 
                value.value = value.value.replace(rep, ''); 
                form = value.value; 
            } 
        }
        const thouthands = (item) => {
            const value = ref(item); 
            var rep = /[-":'a-zA-Zа-яА-Я]/; 
            if (rep.test(value.value)) { 
                value.value = value.value.replace(rep, ''); 
                item = value.value; 
            } 
            item = item.replace(/\s/g, '');
            const copyPrice = ref()
            copyPrice.value=String(item)
            copyPrice.value =  item.replace(/(\d)(?=(\d{3})+([^\d]|$))/g, "$1 ")
            price.value=copyPrice.value
        }
        const error = ref({
                name:false,
                img:false,
                price:false,
            })
            const objectPrice = ref({
                img:'',
                price:'', 
                name:'', 
                text:'',
            })
        const validate = () => {
            const valid = ref(true)
            console.log()
            if(name.value.length!=0){
                objectPrice.value.name=name.value
                valid.value=true
                 error.value.name=false
            }
            else{
                valid.value=false
                error.value.name=true
            }
            if(price.value.length!=0){
                objectPrice.value.price=price.value
                valid.value=true
                error.value.price=false
            }
            else{
                valid.value=false
                error.value.price=true
            }
            if(img.value.length!=0){
                objectPrice.value.img=img.value
                valid.value=true
                error.value.img=false
            }
            else{
                error.value.img=true
                valid.value=false
            }
            objectPrice.value.text=text.value
            return valid.value
        }
        const add = () => {
            if(validate()){
             console.log(objectPrice.value)
            }
        }
        return{
            thouthands,
            price,
            formattedPrice,
            add,
            validate,
            error,
            name,
            img,
            objectPrice,
            text
        }
    },
}
</script>
<style lang="scss">
.catalog-form{
    position: absolute;
    width: 100%;
    max-width: 284px;
    background: #FFFEFB;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
    padding: 24px 24px 8px;
    &__item{
        width: 100%;
        margin-bottom: 16px;
        &-input,
        &-textarea{
            width: calc(100% - 19px) ;
            display: flex;
            flex-direction: column;
            align-items: flex-start;
            height: 36px;
            background: #FFFEFB;
            box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
            border-radius: 4px;
            border: none;
            padding-left: 16px;
             font-family: Source Sans Pro, Helvetica, Arial, sans-serif;
            &::placeholder{
                font-size: 12px;
                line-height: 15px;
                color: #B4B4B4;
            }
        }
         &-textarea{
             padding-top: 10px;
             height: 108px;
             resize: none;
         }
        &-title{
            text-align: left;
            padding-bottom: 4px;
            font-weight: normal;
            font-size: 10px;
            line-height: 13px;
            letter-spacing: -0.02em;
            color: #49485E;
            display: flex;
            svg{
                margin-left: 2px;
            }
        }
        &-button{
            margin: 8px 0px;
            background: #EEEEEE;
            border-radius: 10px;
            padding: 10px 0px;
            font-style: normal;
            font-weight: 600;
            font-size: 12px;
            line-height: 15px;
            text-align: center;
            letter-spacing: -0.02em;
            color: #B4B4B4;
            cursor: pointer;

        }
    }
}
.error{
    border:  1px solid red;
}
</style>