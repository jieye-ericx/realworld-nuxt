<template>
  <div class="article-meta">
    <a href>
      <img :src="article.author.image" />
    </a>
    <div class="info">
      <a href class="author">{{article.author.username}}</a>
      <span class="date">{{article.createdAt}}</span>
    </div>
    <button class="btn btn-sm btn-outline-secondary">
      <i class="ion-plus-round"></i>
      &nbsp;
      Follow {{article.author.username}}
      <span class="counter"></span>
    </button>
    &nbsp;&nbsp;
    <button class="btn btn-sm btn-outline-primary">
      <i class="ion-heart"></i>
      &nbsp;
      Favorite Post
      <span
        v-if="article.favoritesCount!==0"
        class="counter"
      >({{article.favoritesCount}})</span>
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  props:{
    article:{
      type:Object,
      required:true
    }
  },
  components: {}
};
</script>

<style lang="scss" scoped>
</style>
