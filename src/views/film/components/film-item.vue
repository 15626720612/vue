<template>
    <div class="hot-item">
            <img src="https://p1.meituan.net/128.180/movie/740bd990e4af29d537ce324ec2cd08d6300433.jpg" >

            <div class="hot-item-right">

                <div class="hot-item-info">
                    <h4>电影名</h4>
                    <p>观众评 <span>9.0</span></p>
                    <p>主演: 周润发,郭富城,张静初</p>
                    <p>今天182家影院放映2218场</p>
                </div>

                <button v-if="isHot===false" class="bg-bule">预售</button>
                <button v-if="isHot===true">购票</button>
            </div>
        </div>
</template>

<script>
export default {
    props:["isHot"]
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
.hot-item-right .bg-bule{
    background: blue;
}
</style>

