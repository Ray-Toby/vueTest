<template>
  <div>
    <detail-banner
      :sightName="sightName"
      :bannerImg="bannerImg"
      :gallaryImgs="gallaryImgs"
    />
    <detail-header />
    <div class="content">
      <detail-list :list="list" />
    </div>
  </div>
</template>

<script>
import DetailBanner from './components/Banner'
import DetailHeader from './components/Header'
import DetailList from './components/List'
import axios from 'axios'
export default {
  name: 'Detail',
  data () {
    return {
      sightName: '',
      bannerImg: '',
      gallaryImgs: [],
      list: []
    }
  },
  components: {
    DetailBanner,
    DetailHeader,
    DetailList
  },
  mounted () {
    this.getDetailInfo()
  },
  methods: {
    getDetailInfo () {
      axios.get('api/detail.json?' + this.$route.params.id)
        .then(this.handleGetDetailSucc)
    },
    handleGetDetailSucc (res) {
      res = res.data
      if (res.ret && res.data) {
        const data = res.data
        this.sightName = data.sightName
        this.bannerImg = data.bannerImg
        this.gallaryImgs = data.gallaryImgs
        this.list = data.categoryList
      }
    }
  }
}
</script>

<style lang="stylus" scoped>
  .content
    height: 50rem
</style>
