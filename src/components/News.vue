<template>
  <div class="news container w-100 my-5 py-5" data-aos="flip-left" data-aos-duration="2000">
    <h1 class="text-center my-5 fw-bold" >最新消息</h1>
    <div class="row">
      <div class="col-6">
        <div id="carouselExampleSlidesOnly" class="carousel slide" data-bs-ride="carousel" ref="Carousel" >
          <div class="carousel-inner">
            <div class="carousel-item active">
              <div class="carousel-img" :style="{backgroundImage: `url('https://raw.githubusercontent.com/xouoe/Pic/main/fall.jpg')`}">
              </div>
            </div>
            <div class="carousel-item">
              <div class="carousel-img" :style="{backgroundImage: `url('https://raw.githubusercontent.com/xouoe/Pic/main/spring.jpg')`}">
              </div>
            </div>
            <div class="carousel-item">
              <div class="carousel-img" :style="{backgroundImage: `url('https://raw.githubusercontent.com/xouoe/Pic/main/school-start.jpg')`}">
              </div>
            </div>
            <div class="carousel-item">
              <div class="carousel-img" :style="{backgroundImage: `url('https://raw.githubusercontent.com/xouoe/Pic/main/summer.jpg')`}">
              </div>
            </div>
            <div class="carousel-item">
              <div class="carousel-img" :style="{backgroundImage: `url('https://raw.githubusercontent.com/xouoe/Pic/main/face.jpg')`}">
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="col-lg-6 col-md-12 col-sm-12">
        <ul class="list-group" v-for="item in articles.slice(0,5)" :key="item.id">
          <li class="list-group-item my-1 bg-light p-4 border-top-0 border-start-0 border-end-0" aria-current="true"><a href="#" class="text-decoration-none" @click.prevent="articleDetail(item.id)">{{ item.title}}</a></li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import Carousel from 'bootstrap/js/dist/carousel'

export default {
  name: 'TheNews',
  data () {
    return {
      carousel: {},
      articles: [],
      id: ''
    }
  },
  methods: {
    getArticles (page = 1) {
      const api = `${process.env.VUE_APP_API}api/${process.env.VUE_APP_PATH}/articles?page=${page}`
      this.$http.get(api).then(res => {
        this.articles = res.data.articles
      }).catch((err) => {
        this.$pushMessage(err.response)
      })
    },
    articleDetail (id) {
      this.$router.push(`/articles/${id}`)
    }
  },
  mounted () {
    this.carousel = new Carousel(this.$refs.Carousel, { interval: 6000 })
    this.getArticles()
  }
}
</script>

<style lang="scss" scoped>
.news{
  h1 {
    position: relative;
    &::after{
      content:'';
      position: absolute;
      display: inline-block;
      width: 350px;
      border-bottom: 3px solid #000;
      bottom: 0;
      top: 60px;
      left: 36.5%;
    }
    @media(max-width:1919px){
      &::after{
          display: none;
      }
    }
  }
  .carousel{
    @media(max-width:992px){
      display: none;
    }
  }
  .carousel-img{
    height: 400px;
    width: 100%;
    background-size: cover;
    background-position: center;
  }
}

</style>
