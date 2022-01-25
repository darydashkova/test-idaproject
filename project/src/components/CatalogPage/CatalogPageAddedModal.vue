<template>
    <div class="catalog-added">
        <div class="catalog-added__modal">
            <div class="catalog-added__modal-title">Товар успешно добавлен в каталог</div>
            <svg class="catalog-added__modal-close" @click="close" width="14" height="14" viewBox="0 0 14 14" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M14 1.41L12.59 0L7 5.59L1.41 0L0 1.41L5.59 7L0 12.59L1.41 14L7 8.41L12.59 14L14 12.59L8.41 7L14 1.41Z" fill="black"/>
            </svg>
        </div>
    </div>
</template>
<script>

export default {
    emits:['close'],
    props:{},
    setup(props,{emit}) {
     
         const close = () => {
            emit('close')
        }
        return{
            close,
        
        }
    },
}
</script>
<style lang="scss">
    .catalog-added{
        position: fixed;
        background-color: rgba(0, 0, 0, 0.2);
        width: 100%;
        left: 0;
        height: 100%;
        top: 0;
        &__modal{
        position: relative;
        height: 150px;
        width: 400px;
        background-color: rgba(255, 254, 251, 1);
        box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.09);
        top: 40%;
        border-radius: 4px;
        transform: translate(-50%, -40%);
        padding: 0px 16px;
        left: 50%;
        display: flex;
        justify-content: center;
        align-items: center;
        &-title{
           font-weight: 600;
        }
        &-close{
            position: absolute;
            top: 10px;
            right: 10px;
            cursor: pointer;
        }

        
    }
    }
</style>