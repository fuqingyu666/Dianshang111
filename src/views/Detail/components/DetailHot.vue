<script setup>
import { RouterLink } from 'vue-router';
import {getHotGoodsAPI} from '@/apis/detail'
import {useRoute} from 'vue-router'
import { onMounted,ref,computed } from 'vue';
//设置prpos参数，适配不同的title和数据

const props= defineProps({
  hotType:{
    type:Number
  }
})

//适配title 1-24小时热榜  2-周热榜
const TYPEMAP={
  1: '24小时热榜',
  2:'周热榜'
}
const title= computed(()=> TYPEMAP[props.hotType])

const hotList =ref([])
const route =useRoute()
const getHotList =async ()=>{
  const res=await getHotGoodsAPI({
    id:route.params.id,
    type:props.hotType
  })
  hotList.value=res.result
} 

onMounted(() =>getHotList())
</script>


<template>
  <div class="goods-hot">
    <h3>{{title}}</h3>
    <!-- 商品区块 -->
    <router-link to="/" class="goods-item" v-for="item in hotList" :key="item.id">
      <img :src="item.picture" alt="" />
      <p class="name ellipsis">{{item.name}}</p>
      <p class="desc ellipsis">{{item.desc}}</p>
      <p class="price">{{item.price}}</p>
    </router-link>
  </div>
</template>


<style scoped lang="scss">
// 暂时用具体颜色值替代未定义的变量，你可以根据实际情况修改
$helpColor: #007bff; 
$priceColor: #f00; 

.goods-hot {
  h3 {
    height: 70px;
    background: $helpColor;
    color: #fff;
    font-size: 18px;
    line-height: 70px;
    padding-left: 25px;
    margin-bottom: 10px;
    font-weight: normal;
  }

 .goods-item {
    display: block;
    padding: 20px 30px;
    text-align: center;
    background: #fff;

    img {
      width: 160px;
      height: 160px;
    }

    p {
      padding-top: 10px;
    }

   .name {
      font-size: 16px;
    }

   .desc {
      color: #999;
      height: 29px;
    }

   .price {
      color: $priceColor;
      font-size: 20px;
    }
  }
}
</style>