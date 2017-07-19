<template>
    <div>
        <div class="outerContainer">
            <div class="innerContainer" ref="innerContainer">
                <div class="news" ref="newsData">
                    <div>
                        <template v-for="(item,index) in (wonNotices.length?wonNotices:tempDocs)">
                            <span>{{item}}</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
                        </template>
                    </div>
                </div>
            </div>
        </div>
        <div @click="pushNews('hahahahahahahah')">dsdsd</div>
    </div>

</template>

<script>
	export default {
		name: 'instantNewsCss',
		props: {
			wonNotices: {
				type: Array
			}
		},
		methods: {
			pushNews( prizeNews ){
				this.wonNotices.push( prizeNews );
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
    @-webkit-keyframes marquee {
        0% {
            left: 0;
        }
        100% {
            left: -100%;
        }
    }

    @-moz-keyframes marquee {
        0% {
            left: 0;
        }
        100% {
            left: -100%;
        }
    }

    @-ms-keyframes marquee {
        0% {
            left: 0;
        }
        100% {
            left: -100%;
        }
    }

    @-o-keyframes marquee {
        0% {
            left: 0;
        }
        100% {
            left: -100%;
        }
    }

    @keyframes marquee {
        0% {
            left: 0
        }
        100% {
            left: -100%
        }
    }

    @-webkit-keyframes marqueeNews {
        0% {
            left: 100%
        }
        100% {
            left: 0
        }
    }

    @-moz-keyframes marqueeNews {
        0% {
            left: 100%
        }
        100% {
            left: 0
        }
    }

    @-ms-keyframes marqueeNews {
        0% {
            left: 100%
        }
        100% {
            left: 0
        }
    }

    @-o-keyframes marqueeNews {
        0% {
            left: 100%
        }
        100% {
            left: 0
        }
    }

    @keyframes marqueeNews {
        0% {
            left: 100%
        }
        100% {
            left: 0
        }
    }

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
                animation: marqueeNews 150s linear infinite;
                div {
                    position: relative;
                    animation: marquee 150s linear infinite;
                }
            }
        }
    }
</style>