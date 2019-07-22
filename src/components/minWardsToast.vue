<template>
    <div class="wardstoast">
        <span class="title">Chúc mừng nhận</span>
        <div class="wardlist">
            <div class="listitembox">
                <span>
                    <div><img :src="imgone" alt=""></div>
                    <p>{{titleone}}</p>
                </span>
                <span>
                    <div><img :src="imgtwo" alt=""></div>
                    <span></span>
                    <p>{{titletwo}}</p>
                </span>
                <span>
                    <div><img :src="imgthree" alt=""></div>
                    <span></span>
                    <p>{{titlethree}}</p>
                </span>
            </div>
            <p class="double" v-show="showdouble">Thẻ Nhân Đôi, phần thưởng còn lại sẽ nhận gấp đôi, thật tuyệt!</p>
            <p class="toastMsg">Phần thưởng trên đã gửi vào tài khoản bạn, mời kiểm tra!</p>
            <a href="" @click.prevent="closeToast()" class="close"></a>
        </div>
    </div>
</template>

<script>
import {mapState} from "vuex"
import wards from "../config/wards.js"
import wardsImg from "../config/wardsImg.js"
export default {
    data(){
        return{
            showdouble:false
        }
    },
    computed:{
        ...mapState(["lotterylist"]),
        imgone(){
            if(this.lotterylist.length >0){
                var img1 = wardsImg[this.lotterylist[0]]
                return require(`../assets/img/${img1}.png`)
            }
        },
        imgtwo(){
            if(this.lotterylist.length >0){
                var img2 = wardsImg[this.lotterylist[1]]
                return require(`../assets/img/${img2}.png`)
            }
        },
        imgthree(){
            if(this.lotterylist.length >0){
                var img3 = wardsImg[this.lotterylist[2]]
                return require(`../assets/img/${img3}.png`)
            }
        },
        titleone(){
            if(this.lotterylist.length >0){
                return `${wards[this.lotterylist[0]]}`
            }
        },
        titletwo(){
            if(this.lotterylist.length >0){
                return `${wards[this.lotterylist[1]]}`
            }
        },
        titlethree(){
            if(this.lotterylist.length >0){
                return `${wards[this.lotterylist[2]]}`
            }
        }

    },
    watch:{
        lotterylist(val){
            if(val.indexOf(29) > -1){
                this.showdouble = true
            }else{
                this.showdouble = false
            }
        }
    },
    methods:{
        closeToast(){
            this.$emit('hideToast')
        }
    }
}
</script>

<style lang="scss" scoped>
    .wardstoast{
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        z-index: 10000;
        background: #2B0057;
        .title{
            position: absolute;
            top: 3.3rem;
            left: 2.55rem;
            z-index: 100;
            color:#FDFDAC;
            font-weight:bold;
        }
        .wardlist{
            margin:0 auto;
            width: 7.5rem;
            height: 9.16rem;
            background: url("../assets/img/mintaostBg.png") no-repeat center center;
            background-size: 100% auto;
            position: relative;
            .listitembox{
                position: absolute;
                top: 4.3rem;
                left:1.3rem;
                width: 5.1rem;
                height: 1.3rem;
                display: flex;
                //  justify-content:space-between;
                span{
                    display: block;
                    flex:1;
                    text-align: center;
                    >div{
                        display: inline-block;
                        width: .9rem;
                        height: 0.9rem;
                        background-color: #CC00FF;
                        border-radius:.2rem;
                        text-align: center;
                        >img{
                            width: .9rem;
                            height: .9rem;
                        }
                    }
                    >p{
                        color:#5DFFE2;
                        font-size: 80%;
                        text-align: center;
                    }
                }
             
                p{
                    font-size: 80%;
                }
            }
            .double{
                width: 4.58rem;
                height: .49rem;
                position: absolute;
                font-size: 80%;
                top:5.9rem;
                left: 1.5rem;
                color:#FFDB6E;
                text-align: center;
            }
            .toastMsg{
                width: 4.58rem;
                height: .49rem;
                position: absolute;
                font-size: 80%;
                top:6.5rem;
                left: 1.5rem;
                line-height: .45rem;
                text-align: center;
                color:#F7D8FF;
            }
        }
        .close{
            display: block;
            width: 0.71rem;
            height: 0.71rem;
            background: url(../assets/img/close.png) center center;
            background-size: 100% 100%;
            position: absolute;
            bottom: 0;
            left:3.3rem
        }
    }
</style>