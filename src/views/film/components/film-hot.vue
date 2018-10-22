<template>
    <div class="hot-list">
        <FilmItem  v-for="(item,key) in hotFilms" :key="key" :data="item"
        ></FilmItem>
    </div>
</template>

<script>

import FilmItem from"./film-item.vue"
import axios from 'axios'
export default {
    data:() =>{
        return {
            hotFilms:[]
        }
    },
    components: {
        FilmItem
    },
    mounted:function(){
        axios.get("/ajax/movieOnInfoList?token=")
        .then((res) => {
            let {movieList} = res.data;
            //对图片地址进行处理
            movieList = movieList.map((v) => {
                v.img = v.img.replace("w.h","128.180");
                return v;
            })
            this.hotFilms = movieList;
        })
    }
}
</script>

<style>

.hot-list{
    padding:0 10px;
}

.hot-item{
    padding: 10px 0;
    display: flex;
}

.hot-item img{
    display: block;
    width:64px;
    height:90px;
    margin-right: 10px;
}

.hot-item-right{
    display: flex;
    flex: 1;
    justify-content: space-between;
    align-items: center;
    border-bottom: 1px #eee solid;
    padding-bottom: 10px;
}

.hot-item-info p{
    font-size: 13px;
    line-height: 1.8;
    color:#666;
}

.hot-item-info p span{
    color:orange;
    font-size: 16px;
    font-weight: bold;
}

.hot-item-right button{
    height: 27px;
    padding:0 10px;
    background: #f03d37;
    border:none;
    color:#fff;
    border-radius: 4px;
    margin-right: 20px;
}

</style>
