<template>
    <div class="products">
        <div class="products__main">
            <div class="products__main-title">Добавление товара</div>
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
        <div class="products__data">
            <CatalogPageForm></CatalogPageForm>
        </div>
        
        
        
    </div>
</template>

<script>
    import { ref } from 'vue';
    import CatalogPageForm from '../components/CatalogPage/CatalogPageForm'

    export default {
    
        components: {CatalogPageForm},
        setup() {
            const filters = ref([
                {title:'По умолчанию', value:'default'},
                {title:'По возрастанию', value:'min'},
                {title:'По убыванию', value:'max'}
            ])
            const activeFilter = ref()

            const isActiveList = ref(false)

            activeFilter.value=filters.value[0]

            const getFilter = (filter) => {
                activeFilter.value = filter
                console.log(filter)
                console.log(activeFilter.value)
            }

            return {
                filters,
                activeFilter,
                isActiveList,
                getFilter
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
            right: 32px;
            top: 75px;
            display: flex;
            flex-direction: column;
            align-items:flex-start ;
            box-shadow:1px 2px 5px 1px rgba(180, 180, 180, 0.3);
            padding: 10px 20px;
            border-radius: 6px;
            font-weight: normal;
            font-size: 12px;
            line-height: 15px;
            color: #B4B4B4;
            
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
        margin-top: 16px;
    }
}
</style>