<template>
    <div>        
        <div class="container">
            <div v-for="n in 9" class="tab" @click="start(n)" :class="{current: n==current}">{{n==5?'开始':n}}</div >
        </div>
        <timers ref="timers"></timers>
    </div>  

</template>

<script>
const arr = [1,2,3,6,9,8,7,4];
let timer, timer1;
import { swiper, swiperSlide } from 'vue-awesome-swiper'
import timers from './timer'
export default {
    name: 'bookRank',
    components: {
        timers
    },
    data () {
        return {
            current: 1,
            isRuning: false
        }
    },
    methods: {
        async start(n){
            if(n!=5) return;
            if(this.isRuning) {
                return;
            }
            const target = arr[Math.floor(Math.random()*8)]; //模仿从服务器获取奖项
            console.log('target:'+target);
            const setTimer = (speed, isUp) => {
                timer = setInterval(() => {
                    if(this.current == 4) {
                        this.current = arr[0];
                    } else {
                        this.current = arr[arr.indexOf(this.current)+1];
                    }
                    if(speed >= 310) {
                        if(this.current == target) {
                            clearInterval(timer);
                            this.$refs.timers.appendSlide('<div class="swiper-slide">这是一个新的slide</div>');
                        }
                        timer1 = null;  // 清空，否则第二次抽奖时，会一直保持最大速度运行
                        this.isRuning = false;   
                    }else if(speed <= 50) {
                        //设置最大速度运行2秒
                        if(timer1) return; // 保证只创建一个setTimeout
                        timer1 = setTimeout(() => {
                            clearInterval(timer);
                            setTimer(speed+1, false); //最大速度运行两秒后开始减速
                        }, 2000);
                    } else {
                        clearInterval(timer);
                        if(isUp){
                            speed -= 50; //加速度
                            setTimer(speed, true);
                        }else{
                            speed += 20; //减速度
                            setTimer(speed, false);
                        }
                    }
                }, speed);                
            };

            setTimer(300, true);
            this.isRuning = true;
        }
    }
}
</script>

<style scoped>
    #info {
        height: 20px;
        overflow: hidden;
    }
    .container {
        width: 800px;
        height: 800px;
        display: flex;
        flex-flow: row wrap;
        background-color: yellow;
    }
    .tab {
        width: 200px;
        height: 200px;
        background-color: white;
        margin-left: 50px;
    }
    .current {
        background-color: red;
    }
</style>
