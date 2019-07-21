<template>
  <div class="component">
    <div class='list'>
      <template>
        <div class='item' v-for='(v, i) in list' :key='i' @click='jump(v.url)'>
          <div class='item-cover cover-left' v-if='type == "teletext-left" && v.cover'>
            <img :src='v.cover'/>
          </div>
          <div class='item-info'>
            <div class='item-title'>{{v.title}}</div>
            <div class='item-tag' v-if='v.tag && v.tag.length > 0'><span v-for='(tag, j) in v.tag' :key='j' :style='{color: tag.color}'>{{tag.label}}</span></div>
          </div>
          <div class='item-cover cover-right' v-if='type == "teletext-right" && v.cover'>
            <img :src='v.cover'/>
          </div>
        </div>
      </template>
    </div>
  </div>
</template>

<script>
  import {VueExtend} from 'godspen-lib'

  export default {
    mixins: [VueExtend.mixin],
    name: 'list-normal',
    label: process.env.LABEL,
    style: process.env.STYLE,
    props: {
      type: {
        type: String,
        default: 'normal',
        editor: {
          ignore: true
        }
      },
      list: {
        type: Array,
        default () {
          return [
            {
              title: '码良是什么？是如何提供完备的编程接入能力？',
              cover: 'https://gw.alipayobjects.com/zos/rmsportal/qnMZzTAViDGQHHjgyICm.png',
              url: '',
              tag: [
                {
                  label: '运满满',
                  color: 'red'
                },
                {
                  label: '上海前端',
                  color: ''
                },
                {
                  label: '码良',
                  color: ''
                }
              ]
            }
          ]
        },
        editor: {
          ignore: true
        }
      }
    },
    data () {
      return {
      }
    },
    computed: {
    },
    mounted () {
      try {
        this.$parent.$el.style.height = 'auto'
      } catch (e) {
        console.log(e)
      }
    },
    methods: {
      jump (url) {
        if (!url) return
        window.location.href = url
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus" type="text/stylus" scoped>
  .component {
    width: 100%
    .list{
      width: 100%
      padding 0 15px
      .item {
        display: flex;
        align-items: center
        padding 15px 0
        &:not(:last-of-type){
          border-bottom: 1px solid #e9e9e9
        }
      }
      .item-cover{
        width 72px
        height 72px
        img {
          width 100%
          height 100%
        }
      }
      .cover-left{
        margin-right 20px
      }
      .cover-right{
        margin-left 20px
      }
      .item-info{
        flex 1
      }
      .item-title{
        color #333
        font-size 16px
        line-height 1.5
      }
      .item-tag{
        color #999
        font-size 12px
        margin-top 10px
        > span{
          position: relative
          display: inline-block
        }
        > span:not(:last-of-type){
          margin-right 10px
          padding 0 10px 0 0
          &::after{
            position: absolute;
            display: block;
            content: "";
            top: 50%;
            right: 0;
            width: 1px;
            height: 80%;
            -webkit-transform: translateY(-50%);
            -ms-transform: translateY(-50%);
            transform: translateY(-50%);
            background: #e9e9e9;
          }
        }
      }
    }
  }
</style>
