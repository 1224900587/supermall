<template>
    <div class="goodsItem">
        <img :src="goodsItem.show.img" alt="">
        <div>
            <p>{{goodsItem.title}}</p>
            <span class="price">{{goodsItem.price}}</span>
            <span class="cfav">{{goodsItem.cfav}}</span>
        </div>
    </div>
</template>

<script>
export default {
    props:{
        goodsItem:{
            type:Object,
            default(){
                return {}
            }
        }
    }
}
</script>

<style scoped>
    .goodsItem{
        width: 50vw;
    }
    
    .goodsItem img{
        width: 100%;
    }
</style>