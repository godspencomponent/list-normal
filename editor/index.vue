<template>
  <div class="component-editor">
    <div>
      <span>样式：</span>
      <div class='list-type' @click='componentInfo.type = "normal"'>
        <img src="https://ymm-maliang.oss-cn-hangzhou.aliyuncs.com/ymm-maliang/resource/ymm_1563703003962.png" alt="文字列表" />
        <div class="tip">文字列表</div>
        <i class="el-icon-circle-check" v-if='componentInfo.type == "normal"'></i>
      </div>
      <div class='list-type' @click='componentInfo.type = "teletext-left"'>
        <img src="https://ymm-maliang.oss-cn-hangzhou.aliyuncs.com/ymm-maliang/resource/ymm_1563703583604.png" alt="图文列表" />
        <div class="tip">图文列表-左</div>
        <i class="el-icon-circle-check" v-if='componentInfo.type == "teletext-left"'></i>
      </div>
      <div class='list-type' @click='componentInfo.type = "teletext-right"'>
        <img src="https://ymm-maliang.oss-cn-hangzhou.aliyuncs.com/ymm-maliang/resource/ymm_1563703713921.png" alt="图文列表" />
        <div class="tip">图文列表-右</div>
        <i class="el-icon-circle-check" v-if='componentInfo.type == "teletext-right"'></i>
      </div>
    </div>
    <el-card class="box-card">
      <div slot="header" class="clearfix">
        <span>列表项</span>
        <el-button style="float: right; padding: 3px 0" type="text" @click='addItem'>新增一列</el-button>
      </div>
      <div>
        <el-collapse accordion>
          <el-collapse-item :name="i" v-for='(v, i) in componentInfo.list' :key='i'>
            <template slot="title">
              {{v.title}}<i class="el-icon-delete el-collapse-item__arrow del-item" @click.stop='delItem(i)'></i>
            </template>
            <el-form ref="form" label-width="80px" label-position='right' size='mini'>
              <el-form-item label="标题:">
                <el-input v-model="v.title" placeholder="请输入标题"></el-input>
              </el-form-item>
              <el-form-item label="链接:">
                <el-input v-model="v.url" placeholder="请输入链接"></el-input>
              </el-form-item>
              <el-form-item label="封面:">
                <attr-resource type="image" :url.sync="v.cover"></attr-resource>
              </el-form-item>
              <el-form-item label="标签列表:">
                <el-button type="text" @click='addTag(v)'>新增标签</el-button>
                <div class='tag' v-for='(tag, j) in v.tag' :key='j'>
                  <el-input v-model="tag.label" placeholder="标签名"></el-input>
                  <el-color-picker v-model="tag.color" show-alpha></el-color-picker>
                  <i class="el-icon-delete" @click='delTag(v.tag, j)'></i>
                </div>
              </el-form-item>
            </el-form>
          </el-collapse-item>
        </el-collapse>
      </div>
    </el-card>
  </div>
</template>

<script>
  export default {
    name: 'maliangeditor',
    props: {
      componentInfo: { // 固定字段，收集所有属性值
        type: [Object],
        default () {
          return {
            type: 'teletext-left',
            list: []
          }
        }
      }
    },
    data: function () {
      return {
      }
    },
    computed: {
    },
    watch: {
      componentInfo: {
        hanlder: function (v) {
          console.log('editor index', v)
        },
      }
    },
    mounted: function () {
    },
    methods: {
      addItem () {
        let _item = {
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
        this.componentInfo.list.push(_item)
      },
      delItem (i) {
        this.componentInfo.list.splice(i, 1)
      },
      addTag (item) {
        let _tag = {
          label: '运满满',
          color: ''
        }
        item.tag.push(_tag)
      },
      delTag (tag = [], j) {
        tag.splice(j, 1)
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus" type="text/stylus" scoped>
  .component-editor {
    .list-type{
      margin-top 10px
      max-width 250px
      position relative
      border 1px solid #505152
      padding 10px
      border-radius 5px
      img{
        width 100%
      }
      i {
        position absolute
        right 10px
        bottom 15px
        font-size 22px
        color #409EFF
      }
      .tip{
        display: none
        width 100%
        position: absolute
        background-color: rgba(0, 0, 0, 0.7)
        text-align center
        font-size 12px
        padding 3px 0
        bottom 0
        left 0
        color #ccc
      }
      &:hover{
        .tip{
          display: block
        }
      }
    }
    .del-item{
      color #F56C6C
      margin-right 15px
      display none
    }
    .el-collapse-item{
      &:hover{
        .del-item{
          display block
        }
      }
    }
    .tag{
      padding-right 80px
      position relative
      margin-bottom 5px
      .el-color-picker{
        position absolute
        right 30px
        top 0
      }
      i {
        display none
        position absolute
        right 0
        top 5px
        color #F56C6C
        cursor: pointer
      }
      &:hover {
        i {
          display block
        }
      }
    }
  }
</style>
