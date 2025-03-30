<script setup>
import { ElCarousel, ElCarouselItem } from 'element-plus';
import {getBannerApi} from'@/apis/home'
import { onMounted ,ref} from 'vue';

const bannnerList =ref([])

const getBanner =async () =>{
    const res=await getBannerApi()
    bannnerList.value=res.result
}

onMounted(()=> getBanner())

</script>


<template>
  <div class="home-banner">
    <el-carousel height="500px">
      <el-carousel-item v-for="item in bannnerList" :key="item.id">
        <img :src="item.imgUrl" alt="">
      </el-carousel-item>
    </el-carousel>
  </div>
</template>



<style scoped lang='scss'>
.home-banner {
  width: 1240px;
  height: 500px;
  position: absolute;
  left: 0;
  top: 0;
  z-index: 98;

  img {
    width: 100%;
    height: 500px;
  }
}
</style>