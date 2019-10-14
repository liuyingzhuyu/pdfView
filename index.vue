<template>
  <div class="view-contract">
    <!-- 新合同 -->
    <PDF v-if="flag==='h5'" :url="url"/>
    <!-- 法大大合同 -->
    <iframe v-else :src="url" frameborder="0" width="100%" :height="iframeHeight"></iframe>
  </div>
</template>

<script>
let Base64 = require('js-base64').Base64
import PDF from '@/components/PDF'
export default {
  name: 'view-contract',
  data() {
    return {
      flag: this.$route.query.ish5,
      // 如果是新合同，即this.$route.query.ish5==='h5'，则把pdf文件用Base64转成图片用于预览pdf，避免下载
      url:
        this.$route.query.ish5 === 'h5'
          ? Base64.encode(this.$route.query.contractUrl)
          : this.$route.query.contractUrl
    }
  },
  computed: {
    //设置iframe的高度
    iframeHeight() {
      return screen.availHeight - 10
    }
  },
  components: {
    PDF
  }
}
</script>

<style lang="stylus" scoped>
  img{
    width 100%
  }
</style>
