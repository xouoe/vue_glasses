<template>
  <router-view/>
  <PageLoading :active="isLoading"/>
  <div class="bg-light article-purpose">
    <div class="article-title container">
      <h3 class="mb-3">{{ tempArticle.title }}</h3>
    </div>
    <div class="container position-relative article-item d-flex flex-column justify-content-center">
    <div class="image">
        <img class="img" :src="articleImage" alt="最新消息">
    </div>
    <div class="article-content">
      <p class="lh-lg text-secondary">{{ tempArticle.content }}</p>
    </div>
    <div class="notice">
      <h2>注意事項：</h2>
      <ul>
        <li><p>會員與家族定義：</p></li>
        <ol>
          <li>
            <p>舊會員定義：現在已是老薛眼鏡館紅利會員(本活動係指 推薦人)。</p>
          </li>
          <li>
            <p> 新會員定義：未曾到老薛眼鏡館消費的顧客(本活動係指 被介紹人)。</p>
          </li>
          <li>
            <p> 會員家族定義：由同一會員成功推薦之群組(同一推薦人所成立之家族戶)。</p>
          </li>
        </ol>
        <li>
          <p>舊會員推薦新顧客，統計前一個月份推薦的交易筆數與總金額後再進行贈點。</p>
        </li>
        <li>
          <p>本券預計於113/3/15前寄至家族戶之戶長，請依現金抵用券使用說明。</p>
        </li>
        <li>
          <p>本券不得兌換現金、找零，僅限於全台老薛眼鏡館門市配鏡消費使用。</p>
        </li>
        <li>
          <p>配鏡消費後欲使用本券進行折抵時，一副不限一張，可多張數合併使用。</p>
        </li>
        <li>
          <p>老薛眼鏡館保留隨時修改、變更、終止本活動與替換其他等值贈品之權利。</p>
        </li>
        <li>
          <p>對於相關內容有任何疑問，請致電老薛眼鏡館服務專線0800-321-654。</p>
        </li>
        <li>
          <p>老薛眼鏡館公司員工恕不得參加此活動。</p>
        </li>
      </ul>
    </div>
    </div>
    <Section/>
    <Footer class="position-relative end-0 bottom-0"/>
  </div>
  <SocialMedia/>
</template>

<script>
import Footer from '@/components/Footer.vue'
import SocialMedia from '@/components/SocialMedia.vue'
import Section from '@/components/Section.vue'

export default {
  data () {
    return {
      tempArticle: {},
      articleImage: '',
      isLoading: false,
      id: ''
    }
  },
  methods: {
    getArticle () {
      const api = `${process.env.VUE_APP_API}api/${process.env.VUE_APP_PATH}/article/${this.id}`
      this.isLoading = true
      this.$http.get(api).then(res => {
        this.tempArticle = res.data.article
        this.articleImage = res.data.article.imageUrl
        this.isLoading = false
      }).catch((err) => {
        this.$pushMessage(err.response)
      })
    }
  },
  components: { Footer, SocialMedia, Section },
  mounted () {
    this.id = this.$route.params.articleId
    this.getArticle()
  }
}
</script>

<style lang="scss" scoped>
.article-purpose{
  position: relative;
  top: 150px;
  .image{
    width: 100%;
    height: 100%;
    .img{
      max-height: 100%;
      max-width: 100%;
      height: auto;
      background-position: center;
      background-size: cover;
      background-repeat: no-repeat;
    }
  }
  .article-item{
    .article-img{
      width: 100%;
      height: 800px;
      @media (max-width:768px) {
        height: 250px;
      }
      img{
        width: 100%;
      }
    }
    .article-content{
      width: 470px;
      @media (max-width:768px) {
        font-size: 10px;;
        width: 300px;
      }
    }
  }
}
.notice{
  @media (max-width:768px) {
    font-size: 10px;
  }
}
</style>
