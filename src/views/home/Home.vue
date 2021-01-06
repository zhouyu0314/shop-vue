<template>
    <!--    <div id="hy-swiper">-->
    <!--        <div class="swiper" @touchstart="touchStart" @touchmove="touchMove" @touchend="touchEnd">-->
    <!--            <div class="slide">-->
    <!--                <img src="https://s10.mogucdn.com/mlcdn/c45406/180926_45fkj8ifdj4l824l42dgf9hd0h495_750x390.jpg">-->
    <!--            </div>-->
    <!--            <div class="slide">-->
    <!--                <img src="https://s10.mogucdn.com/mlcdn/c45406/180926_31eb9h75jc217k7iej24i2dd0jba3_750x390.jpg">-->
    <!--            </div>-->
    <!--            <div class="slide">-->
    <!--                <img src="https://s10.mogucdn.com/mlcdn/c45406/180919_3f62ijgkj656k2lj03dh0di4iflea_750x390.jpg">-->
    <!--            </div>-->
    <!--            <div class="slide">-->
    <!--                <img src="https://s10.mogucdn.com/mlcdn/c45406/180917_18l981g6clk33fbl3833ja357aaa0_750x390.jpg">-->
    <!--            </div>-->
    <!--        </div>-->


    <!--        <slot name="indicator">-->
    <!--        </slot>-->
    <!--        <div class="indicator">-->
    <!--            <slot name="indicator" v-if="showIndicator && slideCount>1">-->
    <!--                <div v-for="(item, index) in slideCount" class="indi-item" :class="{active: index === currentIndex-1}" :key="index"></div>-->
    <!--            </slot>-->
    <!--        </div>-->

    <!--    </div>-->

    <div>
        <main-swiper :banner="banner"></main-swiper>
    </div>
</template>

<script>
    import MainSwiper from "./MainSwiper";
import {getHomeMultiData} from "./api/home";
    export default {
        name: "Home",
        components: {
            MainSwiper
        },
        created(){
            this.initHomeMultiData();
        },
        mounted() {
            // // 1.操作DOM, 在前后添加Slide，此方法仅仅是初始化轮播图位置，并不参与滚动（3 |0 1 2 3| 0）
            // setTimeout(() => {
            //     this.handleDom();
            //
            //     // 2.开启定时器
            //     this.startTimer();
            // }, 100)
        },
        data() {
            return {
                // interval: 3000,//间隔的毫秒数
                // animDuration: 300,//动画持续时间
                // moveRatio: 0.25,//移动比列，当图片移动超过自身的25%则视为翻页
                // showIndicator: true,//是否显示指示器
                //
                // slideCount: 0, // 元素个数
                // totalWidth: 0, // swiper的宽度
                // swiperStyle: {}, // swiper样式
                // currentIndex: 1, // 当前的index
                // scrolling: false, // 是否正在滚动

                banner:[],
                recommend:[],
            }
        },
        methods: {
            initHomeMultiData(){
                getHomeMultiData().then(res =>{
                    this.banner = res.data.banner.list;
                    this.recommend = res.data.recommend.list;
                })
            }
        }
        // methods:{
        //     startTimer(){
        //         this.playTimer = setInterval(()=>{
        //             this.currentIndex++;//每滚动一次 就要将当前页+1
        //             this.scrollContent(-this.currentIndex * this.totalWidth);
        //         },3000)
        //     },
        //     stopTimer(){
        //         clearInterval(this.playTimer);
        //     },
        //     /**
        //      * 操作DOM, 在DOM前后添加Slide
        //      */
        //     handleDom(){
        //         // 1.获取要操作的元素
        //         let swiperEl = document.querySelector('.swiper');
        //         let slidesEls = swiperEl.getElementsByClassName('slide');
        //         // 2.保存个数
        //         this.slideCount = slidesEls.length;
        //
        //         // 3.如果大于1个, 那么在前后分别添加一个slide
        //         if (this.slideCount > 1) {
        //             let cloneFirst = slidesEls[0].cloneNode(true);//深克隆首节点
        //             let cloneLast = slidesEls[this.slideCount - 1].cloneNode(true);//深克隆尾节点
        //             swiperEl.insertBefore(cloneLast, slidesEls[0]);//在原来的第一个轮播图slidesEls[0] 前面插入一个轮播图 此轮播图来自最后一个 cloneLast
        //             swiperEl.appendChild(cloneFirst);
        //             this.totalWidth = swiperEl.offsetWidth;//获取flex container 的宽度 水平方向 width + 左右padding + 左右border-width
        //             this.swiperStyle = swiperEl.style;
        //             /*
        //             将flex container 视为一个整体，其中有六个flex items（3 0 1 2 3 0），直接按一定size滚动flex container 即可
        //              */
        //         }
        //         // 4.让swiper元素, 显示第一个(目前是显示前面添加的最后一个元素)
        //         //flex container 左移一个flex item的width（3 |0| 1 2 3 0） （|代表视图边框|）
        //         this.setTransform(-this.totalWidth);
        //
        //     },
        //     /**
        //      * 设置滚动的位置
        //      */
        //     setTransform: function (position) {
        //         this.swiperStyle.transform = `translate3d(${position}px, 0, 0)`;
        //         this.swiperStyle['-webkit-transform'] = `translate3d(${position}px), 0, 0`;
        //         this.swiperStyle['-ms-transform'] = `translate3d(${position}px), 0, 0`;
        //     },
        //     /**
        //      * 滚动到正确的位置
        //      */
        //     scrollContent: function (currentPosition) {
        //         // 0.设置正在滚动
        //         this.scrolling = true;
        //
        //         // 1.开始滚动动画
        //        this.swiperStyle.transition ='transform '+ this.animDuration + 'ms';//拿到flex container 的style 设置滚动的过渡动画时间
        //         this.setTransform(currentPosition);//当前依然处于（3 |0| 1 2 3 0）currentPosition=(-1*100px(假设)) -> currentPosition=(-2*100px(假设)) -> （3 0 |1| 2 3 0）
        //
        //         // 2.判断滚动到的位置
        //         this.checkPosition();
        //
        //         // 4.滚动完成
        //         this.scrolling = false
        //     },
        //
        //
        //     /**
        //      * 校验正确的位置
        //      */
        //     checkPosition: function () {
        //         window.setTimeout(() => {
        //             // 1.校验正确的位置
        //             this.swiperStyle.transition = '0ms';
        //             if (this.currentIndex >= this.slideCount + 1) {//this.slideCount=4 如果当前已经滚动到最后一页
        //                 this.currentIndex = 1;//则将当前页初始化到1 （3 0 1 2 3 |0|） -> （3 |0| 1 2 3 0）
        //                 this.setTransform(-this.currentIndex * this.totalWidth);
        //             } else if (this.currentIndex <= 0) {//（|3| 0 1 2 3 0） -> （3 0 1 2 |3| 0）
        //                 this.currentIndex = this.slideCount;
        //                 this.setTransform(-this.currentIndex * this.totalWidth);
        //             }
        //
        //             // 2.结束移动后的回调
        //             this.$emit('transitionEnd', this.currentIndex-1);
        //         }, this.animDuration)
        //     },
        //
        //     /**
        //      * 拖动事件的处理
        //      */
        //     touchStart: function (e) {
        //         // 1.如果正在滚动, 不可以拖动
        //         if (this.scrolling) return;
        //
        //         // 2.停止定时器
        //         this.stopTimer();
        //
        //         // 3.保存开始滚动的位置
        //         this.startX = e.touches[0].pageX;//touches代表当前触摸的手指，可支持多点触控
        //     },
        //
        //     touchMove: function (e) {
        //         // 1.计算出用户拖动的距离
        //         this.currentX = e.touches[0].pageX;
        //         this.distance = this.currentX - this.startX;
        //         let currentPosition = -this.currentIndex * this.totalWidth;
        //         let moveDistance = this.distance + currentPosition;
        //         /*
        //         假设现在时初始页面 currentIndex=1  width=100px   当前位置currentPosition就是-100px （3 |0| 1 2 3 0）
        //         从右向左滑动 100 -> 80 moveDistance （80-100） + -100 = -120
        //          */
        //
        //         // 2.设置当前的位置
        //         this.setTransform(moveDistance);//随着move而翻页
        //     },
        //
        //     touchEnd: function (e) {
        //         // 1.获取移动的距离
        //         let currentMove = Math.abs(this.distance);
        //
        //         // 2.判断最终的距离
        //         if (this.distance === 0) {
        //             return
        //         } else if (this.distance > 0 && currentMove > this.totalWidth * this.moveRatio) { // 右边移动超过0.5 从左向右滑动
        //             this.currentIndex--
        //         } else if (this.distance < 0 && currentMove > this.totalWidth * this.moveRatio) { // 向左移动超过0.5 从右向左滑动
        //             this.currentIndex++
        //         }
        //
        //         // 3.移动到正确的位置
        //         this.scrollContent(-this.currentIndex * this.totalWidth);
        //
        //         // 4.移动完成后重新开启定时器
        //         this.startTimer();
        //     },
        //
        //
        //
        // }
    }
</script>

<style scoped>
    #hy-swiper {
        overflow: hidden;
        position: relative;
    }

    .indicator {
        display: flex;
        justify-content: center;
        position: absolute;
        width: 100%;
        bottom: 8px;
    }

    .indi-item {
        box-sizing: border-box;
        width: 8px;
        height: 8px;
        border-radius: 4px;
        background-color: #fff;
        line-height: 8px;
        text-align: center;
        font-size: 12px;
        margin: 0 5px;
    }

    .indi-item.active {
        background-color: rgba(212, 62, 46, 1.0);
    }


    .swiper {
        display: flex;
    }


    .slide {
        width: 100%;
        flex-shrink: 0; /*不让flex items收缩*/
    }

    .slide img {
        width: 100%;
    }
</style>