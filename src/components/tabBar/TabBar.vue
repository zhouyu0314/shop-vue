<template>
    <div id="tab-bar">
        <tab-bar-item path="/home">
            <img slot="tab-bar-icon" src="../../assets/img/tabBar/home.svg">
            <img slot="tab-bar-icon-active" src="../../assets/img/tabBar/home_active.svg">
            <div slot="tab-bar-text">首页</div>
        </tab-bar-item>

        <tab-bar-item path="/category">
            <img slot="tab-bar-icon" src="../../assets/img/tabBar/category.svg">
            <img slot="tab-bar-icon-active" src="../../assets/img/tabBar/category_active.svg">
            <div slot="tab-bar-text">分类</div>
        </tab-bar-item>

        <tab-bar-item path="/cart">
            <img slot="tab-bar-icon" src="../../assets/img/tabBar/shopcart.svg">
            <img slot="tab-bar-icon-active" src="../../assets/img/tabBar/shopcart_active.svg">
            <div slot="tab-bar-text">购物车</div>
        </tab-bar-item>

        <tab-bar-item path="/profile">
            <img slot="tab-bar-icon" src="../../assets/img/tabBar/profile.svg">
            <img slot="tab-bar-icon-active" src="../../assets/img/tabBar/profile_active.svg">
            <div slot="tab-bar-text">我的</div>
        </tab-bar-item>
    </div>
</template>

<script>
    import TabBarItem from "./TabBarItem";
    export default {
        name: "TabBar",
        components:{
            TabBarItem,
        },
    }
</script>

<style scoped>
    #tab-bar {
        display: flex;
        background-color: #f6f6f6;

        position: fixed;
        left: 0;
        right: 0;
        bottom: 0;

        box-shadow: 0 -1px 1px rgba(100,100,100,.2);
    }
</style>