<template>
  <x-grid :col="columnCount" :elementData="viewModel" v-if="asyncflag"></x-grid>
</template>
<script>
  import { THEME_GETVALUE_GET } from '@/service/api/apiUrl'
  export default {
    name: 'zk-grid',
    data () {
      return {
        viewModel: '',
        asyncflag: false
      }
    },
    props: {
      dataId: {
        type: String
      },
      columnCount: {
        type: Number,
        default: 4
      }
    },
    created () {
      this.ApiGet()
    },
    methods: {
      async  ApiGet () {
        const para = {
          dataId: this.dataId,
          defaultId: '5b406cddfef00000a0000001'
        }
        this.viewModel = await this.$api.get(THEME_GETVALUE_GET, para)
        // console.info('组件数据', this.viewModel)
        this.asyncflag = true
      }
    }
  }
</script>

<style scoped lang="less">
  @import '~_style/index.less'; // 颜色、边框、大小请尽可能的使用变量
  .weui-grid {
  	text-decoration: none;
  	color: @brand;
  	width: 25%;
  	padding: 10px 10px;
  	.weui-grid__icon {
  		margin: 0 auto;
  	}
  }
  .weui-cell:visited {
  	color: #000;
  }
  .weui-grid__label {
  	text-decoration: none;
  	color: #000;
  }
</style>
