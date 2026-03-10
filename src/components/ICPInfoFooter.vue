<script setup>import { ref } from 'vue'

// 从环境变量读取完整公安备案号
const PublicSecurityFullcode = ref(import.meta.env.VITE_PUBLIC_SECURITY_FULLCODE)

// 使用正则提取纯数字部分
const PublicSecurityCode = ref('')
if (PublicSecurityFullcode.value) {
  // 匹配连续12位以上数字（公安备案号数字部分通常为18位）
  const match = PublicSecurityFullcode.value.match(/\d{12,}/)
  PublicSecurityCode.value = match ? match[0] : ''
}

const ICPCode = ref(import.meta.env.VITE_ICP_CODE)
</script>
<template>
  <footer>
    <p>
      <!-- ICP备案链接 -->
      <a :href="`https://beian.miit.gov.cn`" target="_blank">
        {{ ICPCode }}<span v-if="PublicSecurityFullcode">&nbsp;</span>
      </a>
      <!-- 公安备案链接 -->
      <img v-if="PublicSecurityFullcode" src="/beian.png" class="el-image" style="width: 16px; height: 16px; object-fit: contain;">
      <a v-if="PublicSecurityFullcode" :href="`https://www.beian.gov.cn/portal/registerSystemInfo?recordcode=${PublicSecurityCode}`" target="_blank">
        {{ PublicSecurityFullcode }}
      </a>
    </p>
  </footer>
</template>

<style scoped>
/* 备案号链接样式 */
footer a {
  color: #999;
  text-decoration: none;
  transition: color 0.3s ease;
}

footer a:hover {
  color: #e74c3c;
  text-decoration: underline;
}

/* SSL 图标样式 */
.ssl-icon {
  display: inline-block;
  vertical-align: middle;
  margin-left: 10px;
  width: 20px;
  height: 20px;
}

/* 页脚样式 */
footer {
  position: absolute;
  bottom: 20px;
  width: 100%;
  text-align: center;
  font-size: 0.9rem;
  color: #999;
}
</style>