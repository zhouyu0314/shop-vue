<template>
    <div>
        <tab-bar>
            <tab-bar-item path="/home">
                <img slot="tab-bar-icon" src="~assets/img/tabBar/home.svg">
                <img slot="tab-bar-icon-active" src="~assets/img/tabBar/home_active.svg">
                <div slot="tab-bar-text">首页</div>
            </tab-bar-item>

            <tab-bar-item path="/category">
                <img slot="tab-bar-icon" src="~assets/img/tabBar/category.svg">
                <img slot="tab-bar-icon-active" src="~assets/img/tabBar/category_active.svg">
                <div slot="tab-bar-text">分类</div>
            </tab-bar-item>

            <tab-bar-item path="/cart">
                <img slot="tab-bar-icon" src="~assets/img/tabBar/shopcart.svg">
                <img slot="tab-bar-icon-active" src="~assets/img/tabBar/shopcart_active.svg">
                <div slot="tab-bar-text">购物车</div>
            </tab-bar-item>

            <tab-bar-item path="/profile">
                <img slot="tab-bar-icon" src="~assets/img/tabBar/profile.svg">
                <img slot="tab-bar-icon-active" src="~assets/img/tabBar/profile_active.svg">
                <div slot="tab-bar-text">我的</div>
            </tab-bar-item>
        </tab-bar>
    </div>
</template>

<script>
    import TabBar from "../../common/tabBar/TabBar";
    import TabBarItem from "../../common/tabBar/TabBarItem";
    export default {
        name: "MainBar",
        components:{TabBar,TabBarItem},
    }
</script>

<style scoped>

</style>