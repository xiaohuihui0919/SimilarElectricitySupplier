<template>
    <div>
        <!--导航条-->
        <!--<mt-header fixed title="Vue项目"></mt-header>-->
        <mt-header fixed title="Vue项目">
            <router-link to="" slot="left">
                <mt-button v-show="isshow" @click="goBack" icon="back">返回</mt-button>
            </router-link>
        </mt-header>

        <!--切换各个组件的位置-->
        <router-view></router-view>

        <!--tabs内容-->
        <nav class="mui-bar mui-bar-tab">
            <router-link class="mui-tab-item" to="/home">
                <span class="mui-icon mui-icon-home"></span>
                <span class="mui-tab-label">首页</span>
            </router-link>
            <router-link class="mui-tab-item" to="/member">
                <span class="mui-icon mui-icon-email"></span>
                <span class="mui-tab-label">会员</span>
            </router-link>
            <router-link class="mui-tab-item" to="/shopcar">
                <span class="mui-icon mui-icon-contact">
                    <span id="badge" class="mui-badge">0</span>
                </span>
                <span class="mui-tab-label">购物车</span>
            </router-link>
            <router-link class="mui-tab-item" to="/search">
                <span class="mui-icon mui-icon-gear"></span>
                <span class="mui-tab-label">搜索</span>
            </router-link>
        </nav>
    </div>
</template>

<style scoped>

</style>

<script>
    import {vueBus} from './tool/vueBus'
    // 兄弟组件间的传值
    vueBus.$on('sendNumber',function (number) {
        var badge=document.getElementById('badge')
        var tempNumber = badge.innerText - 0;
        tempNumber += number
        badge.innerText=tempNumber
    })
    
    export default {
        data(){
            return {
                isshow:false
            }
        },
        watch:{
            '$route':function (newValue,oldValue) {
                var path=newValue.path;
                // 判断 是否是/home页面
                path=='/home'?this.isshow=false:this.isshow=true
            }
        },
        methods:{
            // 返回上一页
            goBack(){
                this.$router.go(-1)
            }
        }
    }
</script>