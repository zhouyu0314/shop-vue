<template>
    <div @click="itemClick" class="tab-bar-item">
        <div v-if="!isActive">
            <slot name="tab-bar-icon"></slot>
        </div>
        <div v-else>
            <slot name="tab-bar-icon-active"></slot>
        </div>
        <div :style="activeStyle">
            <slot name="tab-bar-text"></slot>
        </div>
    </div>
</template>

<script>
    export default {
        name: "TabBarItem",
        props: {
            path: String,
            activeColor: {type: String, default: 'deepPink'}
            },
        data() {
            return {}
        },
        methods:{
            itemClick(){
                if (!this.isActive) {
                    this.$router.replace(this.path);
                }

            }
        },
        computed: {
            isActive() {
                //如果当前访问的路由路径不是当前页面的 则 isActive = false
                return this.$route.path.indexOf(this.path) !== -1;
            },
            activeStyle() {
                return this.isActive ? {color: this.activeColor} : {};
            }

        }
    }
</script>

<style scoped>
    .tab-bar-item {
        flex: 1;
        text-align: center;
        height: 49px;
        font-size: 14px;
    }

    .tab-bar-item img {
        width: 24px;
        height: 24px;
        margin-top: 3px;
        vertical-align: middle;
        margin-bottom: 2px;
    }
</style>