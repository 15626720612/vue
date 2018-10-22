<template>
    <div class="film-must">
        <div class="film-must-title">
            近期最受期待
        </div>
        <div class="film-top-wrapper">
        <div class="film-top-list">
            <div class="film-top-content">
                <div class="film-top-item" v-for="(item,key) in topItems" :key="key">
                    <img :src="item.img" >
                    <div class="top-item-star">
                        
                    </div>
                    <div class="top-item-imgText" >
                        ❤{{item.wish}}想看
                    </div>
                    <div class="top-item-title">{{item.nm}}</div>
                    <p class="top-item-date">{{item.rt}}</p>
                </div>
            </div>
        </div>
        </div>

        <div class="must-btm-list">
            <div class="film-must-title">
                10月26号 周五
            </div>
            <div class="must-list-wrapper" >
                 <FilmItem :isHot="false" v-for="(item,key) in FilmItem" :key="key" :data="item" ></FilmItem>
            </div>
        </div>

    </div>
</template>
<script>
import FilmItem from"./film-item.vue"
import axios from 'axios'
export default {
    data: ()=>{
        return{
            topItems:[],FilmItem:[]
        }
    },
    components: {
        FilmItem
    },
    mounted: function(){
        axios.get("/ajax/mostExpected?ci=20&limit=10&offset=0&token=")
        .then((res) =>{
            let {coming} = res.data;
            //对图片地址进行处理
            coming = coming.map((v) => {
                v.img = v.img.replace("w.h","128.180");
                return v;
            })
            this.topItems = coming;
        });

        //下面的列表
        axios.get("/ajax/comingList?ci=20&token=&limit=10")
        .then((res) =>{
            let {coming} = res.data;
            //对图片地址进行处理
            coming = coming.map((v) => {
                v.img = v.img.replace("w.h","128.180");
                return v;
            })
            this.FilmItem = coming;
        });

    }

}
</script>
<style>
    .film-must-title{
        padding: 10px;
        font-size: 13px;
        color: #666;
    }
    .film-top-list{
        padding: 0 10px;
    }
    .film-top-item{
        position: relative;
        width: 85px;
        padding: 0 5px;
    }
    .film-top-item :first-child{
        padding-left: 0;
    }
    .film-top-item img{
        display: block;
        /* width: 100%; */
        width: 85px;
        height: 115px;
    }
    .film-top-star{
        position: absolute;
        left: 0;
        top: 0;
        width: 28px;
        height: 28px;
        background: rgba(0,0,0,0.5);
        color: #999;
        text-align: center;
        line-height: 28px;
        border-radius: 0 0 10px 0;
        top: 101px;
    }
    .top-item-imgText{
        background: linear-gradient(rgba(0,0,0,0),rgba(0,0,0,1));
        line-height: 1.5;
        font-size: 12px;
        color: orange;

        position: absolute;
        left: 0;
        top: 101px;
        width: 100%;
        text-align: center;
        font-weight: none;

        display: -webkit-box;-webkit-line-clamp: 1;-webkit-box-orient: vertical;overflow: hidden;
    }
    .top-item-title{
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
        font-weight: bold;
        line-height: 1.5;
        font-size: 13px;
        margin-top: 5px;
    }
    .top-item-date{
        font-size: 13px;
        color: #666;
        line-height: 1.5;
    }

    .film-top-list{
        width: 100%;
        overflow: auto;
        padding: 0 10px;
        box-sizing: border-box;
    }

    .film-top-content{
        display: flex;

    }
    .must-btm-list{
        border-top: 10px #ffffff solid;
    }
    .must-list-wrapper{
        padding: 0 10px;
    }
</style>


