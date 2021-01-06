<template>
    <div>
        <div class="swiper">
            <slot></slot>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Swiper",
        props:{
            timeInterval:{
                type:Number,
                default:3000
            },
          animDuration: {
              type: Number,
          default: 300
          },
        },
        mounted() {
            setTimeout(() => {
                this.handleDom();

                this.startTimer();
            }, 100)
        },
        data() {
            return {
                currentIndex: 1,//默认显示第一个
                flexContainerStyle:{},//flex container 的样式表
                totalWidth:0,
                swiperItemsSize:0,
                scollFlag:false,
            }
        },
        methods: {
            /**
             * 处理dom 初始化flex item位置
             */
            handleDom() {
                //获得所有的flex item
                let swiperItems = document.querySelectorAll(".swiper-item");
                this.swiperItemsSize = swiperItems.length;
                //深克隆其首尾元素
                let firstNode = swiperItems[0].cloneNode(true);
                let lastNode = swiperItems[this.swiperItemsSize - 1].cloneNode(true);

                //在首插入一个lastNode 在尾插入一个firstNode 如果当前处于首页 而此时还手动从左往右划 保证还可以划的动
                let flexContainer = document.getElementsByClassName("swiper")[0];
                flexContainer.appendChild(firstNode);
                flexContainer.insertBefore(lastNode,swiperItems[0]);
                this.flexContainerStyle = flexContainer.style;
                this.totalWidth = swiperItems[0].offsetWidth;
                //滚动到默认的位置
                this.setTransform(-this.totalWidth);
            },


             setTransform(position){
                this.flexContainerStyle.transform = `translate3d(${position}px, 0, 0)`;
                this.flexContainerStyle['-webkit-transform'] = `translate3d(${position}px), 0, 0`;
                this.flexContainerStyle['-ms-transform'] = `translate3d(${position}px), 0, 0`;
            },

            /**
             * 开始滚动
             */
            startTimer(){
                setInterval(()=>{
                    this.scollFlag = true;
                    this.currentIndex++;
                    //修改当前flex container 关于transform的过度动画时间
                    this.flexContainerStyle.transition = `transform ${this.animDuration}ms`;
                    this.setTransform(-this.currentIndex * this.totalWidth);

                    //检查是否滚动到最后一页 因为上面的过度需要时间，所以如果此处检测到currentIndex到了最后一页，则需要等待过度动画完成才能进行无过渡动画的瞬间跳转
                    this.checkScoll();
                    this.scollFlag = false;
                },this.timeInterval)
            },


            checkScoll(){
                /*
                if 我们的排列 3 0 1 2 3 |0| 当前处于最后一个 即currentIndex>=5
                则让 currentIndex=1 即 3 |0| 1 2 3 0
                else if  |3| 0 1 2 3 0 即currentIndex<=0
                 则让 currentIndex=4 即 3 0 1 2 |3| 0
                 */
                setTimeout(()=>{
                    //清除过渡动画时间让其立即翻页
                    this.flexContainerStyle.transition = '0ms';

                    //此处就需要判断currentIndex 如果<=0
                    if(this.currentIndex >= this.swiperItemsSize + 1){
                        this.currentIndex = 1;
                        this.setTransform(-this.currentIndex * this.totalWidth);
                    }else if(this.currentIndex <=0){
                        this.currentIndex =this.swiperItemsSize;
                        this.setTransform(-this.currentIndex * this.totalWidth);
                    }
                },this.animDuration)
            }

        }
    }
</script>

<style scoped>
    .swiper {
        display: flex;
    }
</style>