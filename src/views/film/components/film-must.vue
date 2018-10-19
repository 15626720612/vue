<template>
    <div class="film-must">
        <div class="film-must-title">
            近期最受期待
        </div>
        <div class="film-top-wrapper">
        <div class="film-top-list">
            <div class="film-top-content">
                <div class="film-top-item" v-for="(item,key) in topItems" :key="key">
                    <img src="https://p1.meituan.net/128.180/movie/a05a03a1b1b6c678eb7ef73a8347f4682641527.jpg" >
                    <div class="top-item-star">

                    </div>
                    <div class="top-item-imgText" >
                        123123想看
                    </div>
                    <div class="top-item-title">李嘿嘿嘿龙~~~~</div>
                    <p class="top-item-date">10月29日</p>
                </div>
            </div>
        </div>
        </div>

        <div class="must-btm-list">
            <div class="film-must-title">
                10月26号 周五
            </div>
            <div class="must-list-wrapper" >
                <FilmItem :isHot="false" v-for="(item,key) in topItems" :key="key" ></FilmItem>
            </div>
        </div>

    </div>
</template>
<script>
import FilmItem from"./film-item.vue"
export default {
    data: ()=>{
        return{
            topItems:[1,1,1,1,1,1,1]
        }
    },
    components: {
        FilmItem
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
        width: 100%;
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
        font-weight: bold;
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


