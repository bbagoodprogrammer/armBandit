<template>
    <div class="bandit">
        <a href="./index2.html" class="rules">{{lang.activity_rules}}</a>
        <a href="" class="wardsrod" @click.prevent="showList()">{{lang.draw_record}}</a>
        <a href="" class="knapsack" @click.prevent="goknapsack()" v-if="activeMsg.package === 1">{{lang.my_knapsack}}</a>
        <a href="" class="share" @click.prevent="goShare()" v-if="isShare"></a>
        <my-marquee :lists="textArr"></my-marquee> 
        <turn-table :stime="activeMsg.stime" :etime="activeMsg.etime"></turn-table>
        <cion-buttoms></cion-buttoms>
        <div class="footer">
            <div class="napngay" @click="napngay()"></div>
            <p class="toastMsg">Trong thời gian sự kiện nạp 1 xu nhận 1 bạc</br>
                Bạc dùng để quay thưởng, quay càng nhiều phần</br>
                thưởng càng khủng, tỷ lệ trúng phần thưởng giá trị càng cao!</p>
        </div>
        <loading></loading>
        
        <wards-toast :historyList = historyList ref="wardsToast" v-show="showWardsList" @closeWordToast = "hideList"></wards-toast>
        
    </div>
</template>

<script>
import vietnamLang from "../config/lang.js"
import wards from "../config/wards.js"
import MyMarquee from "../components/MyMarquee.vue"
import TurnTable from "../components/TurnTable.vue"
import CionButtoms from "../components/Buttoms.vue"
import WardsToast from "../components/WardsToast.vue"
import getString from "../utils/getString.js"
import api from "../api/apiConfig.js"
import Loading from "../components/Loading.vue"
import APP from "../utils/openApp.js"
export default {
    components:{MyMarquee,TurnTable,CionButtoms,WardsToast,Loading},
    data(){
        return{
            activeMsg:{},
            lang:vietnamLang,
            textArr:[],
            isShare:false, //是否分享
            historyNum:0,  //抽奖记录当前分页
            historyList:[],
            moreList:true,   //避免下拉加载多次请求
            showWardsList:false
        }
    },
    created(){
        let that = this
        //判断是否为分享环境,请求相应的接口 
        let regstr = getString('token')
        if(regstr){   
            that.isShare = false
        }else{
            that.isShare = true
        }
        that.$store.commit('changShareState',that.isShare) //分享状态
        api.getDefault().then(function(res){ //请求基础数据
            that.activeMsg = res.data.response_data
            that.$store.commit('changcoins',that.activeMsg.coins)  //当前用户老虎币数量
            that.$store.commit('changactState',that.activeMsg.status)  //当前活动状态
            that.activeMsg.lotterylist.forEach(function(item){
                that.textArr.push(`Chúc mừng  ${item.uid}   nhận   ${wards[item.prizeid]} × ${item.num}`)
           })
        })
    },
    mounted(){ //监听滚动事件
        var content = this.$refs.wardsToast.$refs.wardContent
        content.addEventListener('scroll',this.onScroll)
    },
    methods:{
        napngay(){ //跳转储值页面  分享状态下打开APP
            if(!this.isShare){
                 location.href="walletConfig://"
            }else{
                APP()
            }
        },
        onScroll(){  //抽奖记录滚动加载
            var conentHight = this.$refs.wardsToast.$refs.wardContent.clientHeight
            var contentScrollTop = this.$refs.wardsToast.$refs.wardContent.scrollTop
            var contentScrollHeight = this.$refs.wardsToast.$refs.wardContent.scrollHeight
            var that = this
            if(contentScrollHeight - contentScrollTop <= conentHight){ // conentHight + contentScrollTop >= contentScrollHeight -100 寬鬆寫法
                if(that.moreList){
                    that.moreList = false
                    that.historyNum = that.historyList.length
                    api.getHistroy(that.historyNum,"more").then(function(res){
                        if(res.data.response_status.code === 0){
                            var newArr = res.data.response_data.list
                            that.historyList = that.historyList.concat(newArr)
                            that.moreList = true
                        }
                    })
                }
            }
        },
        showList(){ //刷新抽奖记录
            if(this.isShare){ //分享下打开app
                APP()
                return
            }
            var that = this
            that.historyNum = 0
            api.getHistroy(that.historyNum).then(function(res){ //抽奖记录
                if(res.data.response_status.code === 0){
                    var historyList = res.data.response_data.list
                    that.historyList = historyList
                    // that.$store.commit('changhistoryList',historyList)
                    that.showWardsList = true
                    // that.$refs.wardsToast.$refs.wardContent.scrollTop = 0
                }
            })
        },
        hideList(){
            this.showWardsList = false
        },
        goknapsack(){
            if(this.isShare){ //分享下打开app
                APP()
                return
            }
            var u = navigator.userAgent;
            var isAndroid = u.indexOf('Android') > -1 || u.indexOf('Adr') > -1; //android终端
            var isiOS = !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/); //ios终端
            if(isAndroid){
                location.href = `goto:{"controller":"com.utalk.hsing.activity.MyPackActivity","property": {}}`
            }else{
                location.href = `goto:{"controller":"ECMyPackGiftViewController","property": {}}`
            }
            
        },
        goShare(){
            APP()
        }
    }
}
</script>
<style lang='scss'>
    body{
        background-color:#350096;
    }
    .bandit{
        width: 7.5rem;
        position: relative;
        margin: auto;
        background:url(../assets/img/主视觉.png) center 0 no-repeat;
        background-size: 100% auto;
        >a{
            display: block;
            width: 1.19rem;
            height: 0.41rem;
            position: absolute;
            background: url(../assets/img/小按钮.png);
            background-size: 100% 100%;
            right: 0;
            font-size: 80%;
            color:#530003;
            text-align: center;
            line-height: .41rem;
            z-index: 99;
            &.rules{
                top:2.34rem
            }
            &.wardsrod{
                top:2.88rem
            }
            &.knapsack{
                top:3.41rem
            }
            &.share{
                width: 100%;
                height: 1.2rem;
                background: url(../assets/img/share_bar.png);
                background-size: 100% 100%;
                z-index: 999;
                position: fixed;
                top:0;
                left: 0;
                right: 0;
            }
        }
        .footer{
            height: 2rem;
            .napngay{
                width: 2.76rem;
                height: .97rem;
                margin: .5rem auto;
                background: url(../assets/img/nap.png);
                background-size: 100% 100%;
            }
            .toastMsg{
                text-align: center;
                font-size: 80%;
                color:#D5BEFF;
                line-height: .3rem;
            }
        }
    }
</style>


