<template>
    <div class="outerContainer">
        <div class="innerContainer">
            <div class="content" :style="{ top }" ref="content">
                <div v-for="(item,index) in (wonNotices.length?wonNotices:tempDocs)" class="news1" :key="index">
                    {{index + item}}
                </div>
            </div>
        </div>
    </div>
</template>

<script>
	export default {
		name: 'instantNewsCss',
		data () {
			return {
				tempDocs: [
					'恭喜 手机用户_我的用户名视乎看起来非常非常特别长长长 抽中 五等奖 京东E卡（100元） 1张',
					'感谢 liuxinwuq2 的参与，请继续加油哦！',
					'感谢 书香书友f6c56 的参与，请继续加油哦！',
					'恭喜 手机用户_1524 抽中  六等奖 定制手账本 1本',
					'恭喜 手机用户_3527 抽中  二等奖 Kindle 1台',
					'感谢 爱看小说 的参与，请继续加油哦！'
				],
				activeIndex: 0,
				timer: 'timer',
				contentClientHeight: 25
			};
		},
		props: {
			wonNotices: {
				type: Array
			}
		},
		computed: {
			top() {
				return -this.activeIndex * this.contentClientHeight + 'px';
			}
		},
		methods: {
			pushNews( prizeNews ){
				this.wonNotices.push( prizeNews );
			},
			run(){
				this.timer = setInterval( () => {
					if ( parseFloat( window.getComputedStyle( this.$refs.content ).height ) !== this.contentClientHeight ) {
						clearInterval( this.timer );
						this.contentClientHeight = parseFloat( window.getComputedStyle( this.$refs.content ).height );
						this.run();
						return;
					}
					if ( this.activeIndex < this[ this.wonNotices.length ? 'wonNotices' : 'tempDocs' ].length - 1 ) {
						this.activeIndex += 1;
					} else {
						this.activeIndex = 0;
					}
				}, 1000 );
			}
		},
		mounted() {
			console.log( window.getComputedStyle( this.$refs.content ).height );
			console.log( this.$refs.content.offsetHeight );
			this.contentClientHeight = parseFloat( window.getComputedStyle( this.$refs.content ).height );
			this.run();
		}
	};
</script>

<style rel="stylesheet/less" lang="less" scoped>
    .outerContainer {
        margin: 20px 18px 0 16.5px;
        border-radius: 15px;
        background-color: #ff8942;
        border: solid 3px #ff8942;
        text-align: center;
        display: block;
        .innerContainer {
            height: 25px;
            line-height: 25px;
            border-radius: 12.5px;
            background-color: #ff8942;
            border: 2.5px solid #ffcc8d;
            overflow: hidden;
            position: relative;
            .content {
                height: 25px;
                line-height: 25px;
                background-color: transparent;
                position: relative;
                transition: top 0.5s;
                padding: 0 5px;
            }
            .news1 {
                height: 25px;
                font-family: PingFangSC;
                font-size: 13px;
                text-align: center;
                color: #ffe1bb;
                overflow: hidden;
                text-overflow: ellipsis;
                white-space: nowrap;
            }
        }
    }
</style>