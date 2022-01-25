<template>
    <div class="catalog-delete">
        <div  class="catalog-delete__modal">
            <div class="catalog-delete__modal-title">Вы действительно хотите удалить карточку товара?</div>
            <div class="catalog-delete__modal-answer">
                <div class="catalog-delete__modal-answer-delete" @click="del">Удалить</div>
                <div class="catalog-delete__modal-answer-back" @click="close">Отмена</div>
            </div>
        </div>
    </div>
</template>
<script>

export default {
    emits:['del','close'],
    props:{},
    setup(props,{emit}) {
        const del = () => {
            emit('del')
        }
         const close = () => {
            emit('close')
        }
        return{
            close,
            del
        }
    },
}
</script>
<style lang="scss">
    .catalog-delete{
        position: fixed;
        background-color: rgba(0, 0, 0, 0.2);
        width: 100%;
        left: 0;
        height: 100%;
        top: 0;
        &__modal{
        position: relative;
        top: 0;
        height: 150px;
        width: 400px;
        background-color: rgba(255, 254, 251, 1);
        box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.09);
        top: 40%;
        border-radius: 4px;
        transform: translate(-50%, -40%);
        padding: 0px 16px;
        left: 50%;
        &-title{
            padding-top: 20px;
            font-weight: 600;
        }
        &-answer{
            padding-top: 40px;
            display: flex;
            justify-content: space-evenly;
            &-delete{
                background: rgba(227,38,54, 0.6);
                padding: 10px;
                border-radius: 4px;
                transition: 0.3s ease;
                font-size: 12px;
                cursor: pointer;
                &:hover{
                    background: rgba(227,38,54, 1) !important;
                    transition: 0.3s ease;
                }
            }
            &-back{
                box-shadow: 1px 2px 5px 1px rgb(180 180 180 / 30%);
                padding: 10px;
                border-radius: 4px;
                font-size: 12px;
                color: #B4B4B4;
                transition: 0.3s ease;
                cursor: pointer;
                 &:hover{
                     transition: 0.3s ease;
                     color: black;
                }
            }
        }
        
    }
    }
</style>