<template>
  <div class="zk-rater" :style="styles" component-path="core/zk-rater" v-if="asyncflag">
   {{viewModel}}
  </div>
</template>

<script>
  import { THEME_GETVALUE_GET } from '@/service/api/apiUrl'
  import { editSetting } from './property'
  export default {
    name: editSetting.key,
    props: {
      dataId: {
        type: String
      },
      widgetId: {
        type: String
      },
      pageValues: {}
    },
    data () {
      return {
        viewModel: '',
        asyncflag: false,
        styles: {}
      }
    },
    mounted () {
      this.init()
    },
    methods: {
      async  init () {
        if (this.pageValues !== undefined) {
          this.viewModel = this.pageValues
        } else {
          const parameter = {
            dataId: this.dataId,
            defaultId: '5b406cddfef00000a0000001'
          }
          this.viewModel = await this.$api.get(THEME_GETVALUE_GET, parameter)
        }
        this.asyncflag = true
        // console.info('zk-rater数据',this.viewModel)
      }
    }
  }
</script>

<style scoped lang="less">
  @import '~_style/index.less'; 
  .zk-rater {
    font-size: @font-size-base;
  }
</style>

