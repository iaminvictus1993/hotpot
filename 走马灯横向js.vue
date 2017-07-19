<template>
    <div class="outerContainer">
        <div class="innerContainer" ref="innerContainer">
            <div :style="{right}" class="news" ref="newsData">
                实时播报:&nbsp;
                <template v-for="(item,index) in (wonNotices.length?wonNotices:tempDocs)">
                    <span>{{item}}</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
                </template>
            </div>
        </div>
    </div>
</template>

<script>
	export default {
		name: 'instantNews',
		props: {
			wonNotices: {
				type: Array
			}
		},
		watch: {
			wonNotices(){

				// 清除mounted函数生成的定时器
				clearInterval( this.timer );
				this.run();
			}
		},
		mounted(){
			if ( !this.wonNotices.length ) {
				this.run();
			}
		},
		methods: {
			pushNews( prizeNews ){
				clearInterval( this.timer );
				this.wonNotices.unshift( prizeNews );
			},
			run() {

				// 修改数据之后立即使用nextTick，获取更新后的 DOM
				this.$nextTick( () => {
					const initRight = -this.$refs.newsData.offsetWidth + 'px';
					const initInnerContainerOffsetWidth = parseInt( this.$refs.innerContainer.offsetWidth );

					this.right = initRight;
					this.timer = setInterval( () => {

						// 横竖屏切换时，重新开始滚动播放,否则屏幕切换时，left值的设定仍然依据初始屏幕方向的设置
						if ( initInnerContainerOffsetWidth !== parseInt( this.$refs.innerContainer.offsetWidth ) ) {
							clearInterval( this.timer );
							this.run();
							return;
						}
						const numStr = parseInt( this.right );

						if ( initInnerContainerOffsetWidth === numStr ) {
							this.right = initRight;
							return;
						}
						this.right = numStr + 1;
						this.right += 'px';
					}, parseInt( 3500 / initInnerContainerOffsetWidth ) );
				} );
			}
		},
		data () {
			return {
				right: '0px',
				timer: 'timer',
				tempDocs: [
					'恭喜 手机用户_我的用户名视乎看起来非常非常特别长长长 抽中 五等奖 京东E卡（100元） 1张',
					'感谢 liuxinwuq2 的参与，请继续加油哦！',
//					'感谢 书香书友f6c56 的参与，请继续加油哦！',
//					'恭喜 手机用户_1524 抽中  六等奖 定制手账本 1本',
//					'恭喜 手机用户_3527 抽中  二等奖 Kindle 1台',
//					'感谢 爱看小说 的参与，请继续加油哦！'
				]
			};
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
            .news {
                height: 25px;
                font-family: PingFangSC;
                font-size: 13px;
                text-align: center;
                color: #ffe1bb;
                position: absolute;
                white-space: nowrap;
            }
        }
    }
</style>