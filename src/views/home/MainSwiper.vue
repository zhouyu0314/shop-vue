<template>
    <div>
        <swiper>
            <swiper-item v-for="(item,index) in banner " :key="index">
                <a :href="item.link">
                    <img :src="item.image">
                </a>
            </swiper-item>
        </swiper>
    </div>
</template>

<script>
    import {Swiper,SwiperItem} from "./components/index";

    export default {
        name: "MainSwiper",
        components:{
            Swiper,SwiperItem
        },
        props:{
            banner:{
                type:Array,
                default:()=>[]
            }
        }
    }
</script>

<style scoped>

</style>