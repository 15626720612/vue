<template>
    <div class="likes-wrapper">
        <div class="likes-title">
            猜你喜欢
        </div>
        

        <div class="like-list">
            
            <!-- 猜你喜欢 start -->
            <div class="like-item" v-for="(item, key) in likes" :key="key">
                <img :src="item.img">
                
                <div class="like-item-right">
                    <div>
                        <div class="like-title">
                            {{item.title}}
                        </div>
                        <p>
                            {{item.address}}
                        </p>
                    </div>

                    <div class="like-bottom">
                        <span>{{item.price}}元</span>
                        <em>已售 {{item.last}} </em>
                    </div>
                </div>

            </div>
            <!-- 猜你喜欢 end -->

        </div>

    </div>
</template>

<script>
export default {
    name: "like_list",
    data: () => {
        return {
            likes: [{
                img: "http://p1.meituan.net/200.0/dpdeal/bdbcb13417a2008ab25f8eb51f7818af7221.png",
                title: "巴喜阳光BBQ自助餐厅",
                address: "[体育中心]单人自助午餐",
                price: "58",
                last: "124124124"
            },
            {
                img: "http://p1.meituan.net/200.0/dpdeal/bdbcb13417a2008ab25f8eb51f7818af7221.png",
                title: "巴喜阳光BBQ自助餐厅2",
                address: "[体育中心]单人自助午餐2",
                price: "30",
                last: "123123"
            }]
        }
    }
}
</script>
<style>
    .likes-wrapper{
        border-top:10px #eee solid;
        padding:0 10px;
    }

    .likes-title{
        height:40px;
        line-height: 40px;
        border-bottom: 1px #eee solid;
    }

    .like-item{
        padding:10px 0;
        border-bottom:1px #eee solid;
        display: flex;
    }

    .like-item img{
        width:90px;
        height:90px;
        display: block;
        margin-right:10px;
    }

    .like-item-right{
        display: flex;
        /*把方向改为上下*/
        flex-direction: column;
        /* 上下贴边对齐 */
        justify-content: space-between;
        flex:1;
    }

    .like-item-right p{
        font-size: 12px;
        color:#666;
        margin-top: 5px;
    }

    .like-bottom span{
        color: #06c1ae;
        font-size: 18px;
    }

    .like-bottom em{
        font-style: normal;
        font-size: 12px;
        color:#666;
        float: right;
    }

</style>


