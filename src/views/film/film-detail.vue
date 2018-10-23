<template>
    <div>
        <div class="detail-header">
            <span @click="handleBack"></span>
            {{this.detail.nm}}
        </div>
        <div class="detail-info">
            <img class="detail-info-bg" :src="this.detail.img">
            <!-- 详情内容 -->
            <div class="detail-content">
                <img :src="this.detail.img">
            <div class="detail-content-right">
                <h4>{{this.detail.nm}}</h4>
                <div class=".detail-en-name">
                    {{this.detail.enm}}
                </div>
                <p><span>{{this.detail.sc}}</span>({{this.detail.snum}}人评分)</p>
                <p>{{this.detail.cat}}</p>
                <p>{{this.detail.src}}/{{this.detail.dur}}分钟</p>
                <p>{{this.detail.pubDesc}}</p>
            </div>
            </div>
        </div>
        <!-- 日期选择 -->
        <div class="detail-date-wrapper">
            <div class="detail-date-list">

                <div class="detail-date-item" 
                v-for="(item,key) in dates" 
                :key="key"
                :class="{active: currentDate === key}"
                @click="handleDateChange(key)">
                    {{item.date}}
                </div>
            </div>
        </div>
        <!-- 条件选择 -->
        <div class="detail-condition">
            <div class="detail-condition-item">
                全城
            </div>
            <div class="detail-condition-item">
                品牌
            </div>
            <div class="detail-condition-item">
                特色
            </div>
        </div>
        <!-- 电影院列表 -->
        <div class="film-address-list">
            <div class="film-address-item" v-for="(item,key) in address" :key="key">
                <h4>{{item.nm}} <span>{{item.sellPrice}}<i>元起</i></span></h4>
                <div class="address-bar">
                    <div class="address-bar-right">
                        {{item.addr}}
                    </div>
                    <p>{{item.distance}}</p>
                </div>
                <div class="address-tags">
                    <span class="yellow" v-for="(tag,key) in item.tag.hallType" :key="key">{{tag}}</span>
                </div>
                <p class="address-action">
                    {{item.promotion.ardPromotionTag}}
                </p>
                <p class="address-action">
                    近期场次:{{item.showTimes}}
                </p>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import moment from 'moment'
export default {
    methods: {
        handleBack: function(){
            window.history.back();
        },
        handleDateChange: function(index){
            this.currentDate = index;
        }
    },
    data: ()=>{
        return{
            dates:[],
            address:[],
            detail: {},
            currentDate:0
        }
    },
    mounted: function(){
        //每次进入页面都滚动到最顶部
        window.scrollTo(0,0);
        // console.log(this.$route)
        const id = this.$route.params.id;
        const url = "/ajax/detailmovie?movieId=" + id;

        axios.get(url).then((res) => {
            const {detailMovie} = res.data;
            detailMovie.img = detailMovie.img.replace("w.h","148.208");
            this.detail = detailMovie;
        })

        //请求电影院列表
        axios.post("/ajax/movie?forceUpdate=1540275365380",{
            movieId: id,
            day: moment().format('YYYY-MM-DD'), //获取当天的时间
            offset: 0,
            limit: 20,
            districtId: -1,
            lineId: -1,
            hallType: -1,
            brandId: -1,
            serviceId: -1,
            areaId: -1,
            stationId: -1,
            updateShowDay: true,
            reqId: 1540177250401,
            cityId: 20,
        }).then(res =>{
            const {showDays,cinemas}=res.data;
            //初始化dates
            this.dates = showDays.dates;
            //初始化电影院列表
            this.address = cinemas;
        })
    }
}
</script>

<style>
    .detail-header{
        height: 50px;
        line-height: 50px;
        color: #fff;
        text-align: center;
        background: #06c1ae;
        font-size: 18px;
        border-bottom: 1px #666 solid;

        position: relative;
        
    }
    .detail-header::before{
        display: block;
        content: "";
        width: 15px;
        height: 15px;
        border-bottom:2px #fff solid;
        border-left: 2px #fff solid;
        transform: rotate(45deg);
        /* background: #fff; */
        position: absolute; 
        left: 15px;
        top: 50%;
        margin-top: -8px;
    }
    .detai-header span{
        display: block;
        content: "";
        width:15px;
        height: 15px;
        border-bottom: 2px #fff solid;
        border-left:2px #fff solid;
        transform: rotate(45deg);

        position: absolute;
        left:15px;
        top:50%;
        margin-top: -8px;
    }
    /* 电影详情 */
    .detail-info{
        position: relative;
        height: 188px;
        overflow: hidden;
        box-shadow: 0 0 20px 20px rgba(0, 0, 0,0.5) inset;
    }
    .detail-info-bg{
        display: block;
        width: 100%;
        filter: blur(15px); 
    }
    /* 详情内容 */
    .detail-content{
        padding: 16px 10px;
        position: absolute;
        left: 0;
        top: 0;
        width: 100%;
        box-sizing: border-box;
        display: flex;
        background: rgba(0, 0, 0, 0.2);
        height: 100%;
    }
    .detail-content img{
        display: block;
        height: 150px;
    }
    .detail-content-right{
        margin-left: 10px;
        color: #fff;
    }
    .detail-content-right h4{
        font-size: 18px;
    }
    .detail-en-name{
        font-size: 12px;
        margin-top: 5px;
    }
    .detail-content-right p{
        line-height: 1.8;
        font-size: 13px;
    }
    .detail-content-right::after{
        display: block;
        content: "";
        width: 10px;
        height: 10px;
        border-top: 2px #fff solid;
        border-right: 2px #fff solid;
        transform: rotate(45deg);
        position: absolute;
        right: 10px;
        top: 50%;
        margin-top: -5px;
    }
    .detail-content-right p span{
        font-weight: bold;
        color: orange;
        font-size: 18px;

    }
    /* 日期列表 */
    .detail-date-wrapper{
        overflow-x: auto; /* x轴在滚动条 */
    }
    .detail-date-wrapper::-webkit-scrollbar{
        width: 0;
        height: 0;
    }
    .detail-date-list{
        display: flex;
        height: 43px;
        line-height: 43px;
        font-size: 13px;
        color: #666;
        border-bottom: 1px #eee solid;
    }
    .detail-date-item{
        width: 115px;
        flex-shrink: 0;
    }
    .detail-date-item.active{
        color:red;
        border-bottom:2px red solid;
    }
    /* 条件选择 */
    .detail-condition{
        display: flex;
        justify-content: space-around;
        height: 43px;
        line-height: 23px;
        border-bottom: 1px #eee solid;
        font-size: 13px;
        color: #666;
        padding: 10px 0;
        box-sizing: border-box;
    }
    .detail-condition-item{
        flex: 1;
        text-align: center;
        border-right: 1px #eee solid;
    }
    .detail-condition-item:last-child{
        border-right: none;
    }
    .detail-condition-item::after{
        display: inline-block;
        content: "";
        width: 0px;
        height: 0px;
        border-left: 5px transparent solid;
        border-right: 5px transparent solid;
        border-top: 5px #999 solid;
        /* background: #000; */
        position: relative;
        top: -2px;
    }
    /* 电影院 */
    .film-address-list{
        padding-left:5px; 
    }
    .film-address-item{
        border-bottom: 1px #eee solid; 
        padding-bottom: 10px;
    }
    .film-address-item h4{
        margin-top:5px;
        line-height: 23px;
        font-size: 16px;
        font-weight: normal; 
    }
    .film-address-item span{
        color: red;
        font-size: 14px;
        margin-left: 0px; 
    }
    .film-address-item h4 span{
        margin-left: 5px;
        font: 20px;
    }
    .film-address-item i{
        margin-left: 0px;
        font-style: normal;
    }
    .address-bar{
        margin-top:5px; 
        font-size: 13px;
        color: #666;
        display: flex;
    }
    .address-bar-right{
        margin-top:0px; 
        width: 85%;
        overflow: hidden;
    }
    .address-tags{
        margin-top:5px; 
        margin-left: 0px;
    }
    .address-tags .yellow{
        color: orangered;
        border:1px orangered solid;
        border-radius: 3px;
    }
    .address-tags .cyen{
        color:cyan;
        border:1px cyan solid;
        border-radius: 3px;
        margin-left: 10px;
    }
    .address-action{
        margin-top:5px; 
        font-size: 10px;
        color: #666;
    }
</style>
