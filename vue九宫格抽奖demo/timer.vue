<template>
    <div>        
        <div id="info">
            <swiper :options="swiperOption" ref="mySwiper">
                <swiper-slide v-for="n in 5">{{'恭喜xxxx获得拖鞋一双'+n}}</swiper-slide>
            </swiper>
        </div>
    </div>  

</template>

<script>
import { swiper, swiperSlide } from 'vue-awesome-swiper'
export default {
    name: 'timer',
    components: {
        swiper,
        swiperSlide
    },
    data () {
        return {
            swiperOption: {
                direction : 'vertical',
                loop : true,
                autoplayDisableOnInteraction : false,
                autoplay: 500,
                height:20
            }
        }
    },
    methods: {
        appendSlide(str) {
            this.$refs.mySwiper.swiper.appendSlide(str);
        }
    }
}
</script>

<style scoped>
    #info {
        height: 20px;
        overflow: hidden;
    }
    
</style>
