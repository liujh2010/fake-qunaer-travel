<template>
  <div class="list" ref="wrapper">
    <div>
      <div class="area">
        <div class="title border-topbottom">当前城市</div>
        <div class="button-list">
          <div class="button-wrapper">
            <div class="button">{{this.currentCity}}</div>
          </div>
        </div>
      </div>
      <div class="area">
        <div class="title border-topbottom">热门城市</div>
        <div class="button-list">
          <div
            class="button-wrapper"
            v-for="hotCity of hot"
            :key="hotCity.id"
            @click="handleCityClick(hotCity.name)"
          >
            <div class="button">{{hotCity.name}}</div>
          </div>
        </div>
      </div>
      <div class="area" v-for="(item, key) of cities" :key="key" :ref="key">
        <div class="title border-topbottom">{{key}}</div>
        <div class="item-list">
          <div
            class="item border-bottom"
            v-for="city of item"
            :key="city.id"
            @click="handleCityClick(city.name)"
          >{{city.name}}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import BScroll from 'better-scroll'
import { mapState, mapMutations } from 'vuex'
export default {
  name: 'CityList',
  props: {
    hot: Array,
    cities: Object,
    letter: String
  },
  methods: {
    ...mapMutations(['changeCity']),
    handleCityClick (city) {
      this.changeCity(city)
      this.$router.push('/')
    }
  },
  computed: {
    ...mapState({
      currentCity: 'city'
    })
  },
  watch: {
    letter () {
      let element = this.$refs[this.letter][0]
      this.scroll.scrollToElement(element)
    }
  },
  mounted () {
    this.scroll = new BScroll(this.$refs.wrapper)
  }
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles'

.border-topbottom
  &:before
    border-color: #ccc
  &:after
    border-color: #ccc
.border-bottom
  &:before
    border-color: #ccc
.title
  line-height: 0.54rem
  background: #eee
  padding-left: 0.2rem
  color: #666
  font-size: 0.26rem
.list
  overflow: hidden
  position: absolute
  top: 1.59rem
  right: 0
  left: 0
  bottom: 0
  .button-list
    overflow: hidden
    padding: 0.1rem 0.6rem 0.1rem 0.1rem
    .button-wrapper
      float: left
      width: 33.3%
      .button
        margin: 0.1rem
        padding: 0.1rem 0
        text-align: center
        border: 0.02rem solid #ccc
        border-radius: 0.06rem
  .item-list
    .item
      padding-left: 0.2rem
      line-height: 0.76rem
</style>
