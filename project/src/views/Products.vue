<template>
    <div class="products">
        <div class="products__main">
            <div class="products__main-title">Добавление товара</div>
            <div class="products__main_mobile">
                <div class="products__main-select" :class="{'products__main-select_active':isActiveList}" 
                @click="isActiveList=!isActiveList">
                    {{activeFilter.title}}
                    <svg  width="8" height="6" viewBox="0 0 8 6" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M7.48532 1.24264L4.24268 4.48528L1.00003 1.24264" stroke="#B4B4B4"/>
                    </svg>
            </div>
             <div class="products__main-list" v-if="isActiveList">
                    <div class="products__main-list-item" v-for="(filter, index) in filters" :key="index" @click="isActiveList=false, getFilter(filter)">
                        {{filter.title}}
                    </div>
                </div>
            </div>
            
        </div>
        <div class="products__data">
            <CatalogPageForm @newProduct='postProduct' ></CatalogPageForm>
            <CatalogPageProducts :data="copyProducts" @openModal='getIndex'></CatalogPageProducts>
        </div>
        <CatalogPageDelete v-if="isOpenModalDelete" @del="deleteCard" @close="isOpenModalDelete = false, cartToDelete = null"></CatalogPageDelete>
    </div>
</template>

<script>
    import { ref, onMounted } from 'vue';
    import CatalogPageForm from '../components/CatalogPage/CatalogPageForm'
    import CatalogPageProducts from '../components/CatalogPage/CatalogPageProducts'
    import CatalogPageDelete from '../components/CatalogPage/CatalogPageDelete.vue'
            
    export default {
    
        components: {CatalogPageForm, CatalogPageProducts, CatalogPageDelete},
        setup() {
            const isOpenModalDelete = ref(false);
            const filters = ref([
                {title:'По умолчанию', value:'default'},
                {title:'По возрастанию', value:'min'},
                {title:'По убыванию', value:'max'}
            ])
            const deleteCard = () => {
                 products.value.splice( cartToDelete.value, 1)
                 isOpenModalDelete.value = false
            }
            const cartToDelete = ref()

            const getIndex = (index) => {
                cartToDelete.value = index
                isOpenModalDelete.value = true
            }
        const products = ref([
                {img:'https://html5book.ru/wp-content/uploads/2014/07/html_images.png', price:150000, 
                name:'Товар1', text:'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк'},
                {img:'https://html5book.ru/wp-content/uploads/2014/07/html_images.png', price:1400, 
                name:'Товар1', text:'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк'},
                {img:'https://html5book.ru/wp-content/uploads/2014/07/html_images.png', price:1400, 
                name:'Товар1', text:'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк'},
                {img:'https://html5book.ru/wp-content/uploads/2014/07/html_images.png', price:1400, 
                name:'Товар1', text:'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк'},
                {img:'https://html5book.ru/wp-content/uploads/2014/07/html_images.png', price:1900, 
                name:'Товар1', text:'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк'},
                {img:'https://html5book.ru/wp-content/uploads/2014/07/html_images.png', price:1400, 
                name:'Товар1', text:'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк'},
                {img:'https://html5book.ru/wp-content/uploads/2014/07/html_images.png', price:1400, 
                name:'Товар1', text:'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк'},
                {img:'https://html5book.ru/wp-content/uploads/2014/07/html_images.png', price:1400, 
                name:'Товар1', text:'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк'},
            ])
            const activeFilter = ref()

            const isActiveList = ref(false)

            activeFilter.value=filters.value[0]

            const getFilter = (filter) => {
                activeFilter.value = filter
                if(filter.value == 'min'){
                   copyProducts.value.sort((prev, next) => prev.price - next.price);
                  
                }
                 else if(filter.value == 'max'){
                   copyProducts.value.reverse(function(a, b) { return a.price < b.price });
                }
                else {
                    copyProducts.value = products.value.slice();
                }

            }

            window.onbeforeunload = () => { 
             localStorage.setItem('products', JSON.stringify(products.value)) 
            }
             const copyProducts = ref();
             copyProducts.value = products.value.slice();
            onMounted(()=>{
                if(JSON.parse(localStorage.getItem("products"))!=null){
                   products.value=JSON.parse(localStorage.getItem("products")); 
                }
            })
            const postProduct = (i) => {
                 products.value.push(i)
                 copyProducts.value = products.value.slice();
               
            }
            
            return {
                filters,
                activeFilter,
                isActiveList,
                getFilter,
                products,
                postProduct,
                isOpenModalDelete,
                deleteCard,
                getIndex,
                cartToDelete,
                copyProducts
                
            }
            
        },
    }
</script>

<style lang="scss">
.products{
    padding: 32px;
    
    &__main{
        display: flex;
        justify-content: space-between;
        @media (max-width: 768px) {
            flex-direction: column;
            &_mobile{
                width: 100%;
                display: flex;
                justify-content: center;
                position: relative;
            }
        }
        &-title{
            font-style: normal;
            font-weight: 600;
            font-size: 28px;
            line-height: 35px;
            color: #3F3F3F;
            position: relative;
        
        }
       &-select{
            box-shadow:1px 2px 5px 1px rgba(180, 180, 180, 0.3);
            padding: 10px 16px;
            border-radius: 6px;
            font-weight: normal;
            font-size: 12px;
            line-height: 15px;
            color: #B4B4B4;
            transition: 0.3s ease;
             @media (max-width: 768px) {
                 max-width: 300px;
                 width: 100%;
            }
            cursor: pointer;
            svg{
                margin-left: 5px;
                path{
                 transition: 0.3s ease;   
                }
                
            }
            &:hover,
             &_active{
                color: #3F3F3F;
                transition: 0.3s ease;
                svg path {
                     stroke: #3F3F3F;
                     transition: 0.3s ease;
                }
            }
            &_active{
                svg{
                    transform: rotatex(180deg);
                }
                
            }
       }
       &-list{
            position: absolute;
            background: #FFFEFB;
            right: 15px;
            top: 75px;
            display: flex;
            z-index: 99;
            flex-direction: column;
            align-items:flex-start ;
            box-shadow:1px 2px 5px 1px rgba(180, 180, 180, 0.3);
            padding: 10px 20px;
            border-radius: 6px;
            font-weight: normal;
            font-size: 12px;
            line-height: 15px;
            color: #B4B4B4;
             @media (max-width: 400px) {
               top: 50px;
                width: calc(100% - 40px);
                max-width: 100%;
                right: 0%;
                transform: translateX(0%);
            }
            @media (min-width: 401px) and (max-width: 768px) {
               top: 50px;
                width: 100%;
                max-width: 292px;
                left: 50%;
                transform: translateX(-50%);
            }
            &-item{
                padding: 6px 0px 0px;
                transition: 0.3s ease;
                cursor: pointer;
                 &:hover{
                color: #3F3F3F;
                transition: 0.3s ease;
                }
            }
    }
    }
    &__data{
        position: relative;
        margin-top: 16px;
        display: flex;
         @media (max-width: 768px) {
        justify-content: center;
        }
    }
}
</style>