<template>
  <div>
    <div class="home-page">
      <div class="banner">
        <div class="container">
          <h1 class="logo-font">conduit</h1>
          <p>A place to share your knowledge.</p>
        </div>
      </div>

      <div class="container page">
        <div class="row">
          <div class="col-md-9">
            <div class="feed-toggle">
              <ul class="nav nav-pills outline-active">
                <li class="nav-item">
                  <a class="nav-link disabled" href>Your Feed</a>
                </li>
                <li class="nav-item">
                  <a class="nav-link active" href>Global Feed</a>
                </li>
              </ul>
            </div>

            <div class="article-preview" v-for="(article,i) in articles " :key="i">
              <div class="article-meta">
                <a href="profile.html">
                  <img :src="article.author.image" />
                </a>
                <div class="info">
                  <a href class="author">{{article.author.username}}</a>
                  <span class="date">{{article.createdAt}}</span>
                </div>
                <button class="btn btn-outline-primary btn-sm pull-xs-right">
                  <i class="ion-heart"></i> {{article.favoritesCount}}
                </button>
              </div>
              <a href class="preview-link">
                <h1>{{article.title}}</h1>
                <p>{{article.description}}</p>
                <span>Read more...</span>
              </a>
            </div>
          </div>

          <div class="col-md-3">
            <div class="sidebar">
              <p>Popular Tags</p>

              <div class="tag-list">
                <a href class="tag-pill tag-default" v-for="(tag,i) in tags" :key="i">{{tag}}</a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  components: {},
  async asyncData({$axios}) {
    //由于下面两个请求没有依赖关系，按序执行浪费时间，用promise.all来一起执行，返回一个数组，按序存储各任务的结果
    // const { data:articleData } = await $axios.get(`/api/articles`);
    // const { data:tagsData } = await $axios.get(`/api/tags`);
    const [tagsData,articleData] =await Promise.all([$axios.get(`/api/tags`),$axios.get(`/api/articles`)])
    // console.log(articleData.data);
    
    return {
      articles:articleData.data.articles,
      tags:tagsData.data.tags
    };
  },
  data() {
    return {};
  }
};
</script>

<style>
</style>
