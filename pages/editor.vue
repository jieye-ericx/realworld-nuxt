<template>
  <div class="editor-page">
    <div class="container page">
      <div class="row">
        <div class="col-md-10 offset-md-1 col-xs-12">
          <form>
            <fieldset>
              <fieldset class="form-group">
                <input
                  v-model.lazy="article.title"
                  type="text"
                  class="form-control form-control-lg"
                  placeholder="Article Title"
                />
              </fieldset>
              <fieldset class="form-group">
                <input
                  v-model.lazy="article.description"
                  type="text"
                  class="form-control"
                  placeholder="What's this article about?"
                />
              </fieldset>
              <fieldset class="form-group">
                <textarea
                  class="form-control"
                  rows="8"
                  v-model.lazy="article.body"
                  placeholder="Write your article (in markdown)"
                ></textarea>
              </fieldset>
              <fieldset class="form-group">
                <input
                  v-model.lazy="tagText"
                  type="text"
                  class="form-control"
                  placeholder="Enter tags"
                  @keyup.enter="onAddTag"
                />
                <div class="tag-list">
                  <span @click="article.tagList.splice(i,1)" v-for="(item,i) in article.tagList" :key="i" class="tag-default tag-pill">
                    <i class="ion-close-roune" >{{item}}</i>
                  </span>
                </div>
              </fieldset>
              <button
                @click="onCreate"
                class="btn btn-lg pull-xs-right btn-primary"
                type="button"
              >Publish Article</button>
            </fieldset>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  middleware: "authenticated",
  data() {
    return {
      article: {
        title: "",
        description: "",
        body: "",
        tagList: []
      },
      tagText:''
    };
  },
  components: {},
  methods: {
    async onCreate() {
      const { data } = await this.$axios.post("/api/articles", {
        article: this.article
      });
      // console.log(data);
      this.$router.push(`/article/${data.article.slug}`)

    },
    onAddTag(){
      const tagText=this.tagText
      const {tagList}=this.article
      if(!tagText.length){
        return
      }
      if(this.article.tagList.includes(tagText)){
        return
      }
      this.article.tagList.push(tagText)
      this.tagText=''
    }
  }
};
</script>

<style lang="scss" scoped>
</style>
