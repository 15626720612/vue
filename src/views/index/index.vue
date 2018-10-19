<template>
<!-- 这是一个div -->
  <div id="app">
    <IndexHeader></IndexHeader>

    <Category></Category>

    <LikeList></LikeList>
  </div>
</template>

<script>

import IndexHeader from "../../components/index-header.vue"
import Category from "../../components/category.vue"
import LikeList from "../../components/like-list.vue"

export default {
    name: "index",
    components: {
        IndexHeader,
        Category,
        LikeList
    },
}
</script>
