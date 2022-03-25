<template>
  <div>
    <h2 class="danger">
      <i class="fa-regular fa-circle-xmark"></i>
      当前您的浏览器暂时没有使用 HTTP/3
    </h2>
    <p>请您检查浏览器设置或网络配置</p>
    <br />
    <p>
      Chrome用户请打开<code>chrome://flags/#enable-quic</code>开启QUIC功能；<br />
      Firefox用户请打开<code>about:config</code>，在<code>network.http.http3.enabled</code>中设置为<code>true</code>
    </p>
    <p>如果您在使用代理服务器，请确保其支持UDP传输功能</p>
    <p>HTTP/3 目前还没有广泛使用，您可以稍后重试，有可能因为网络问题浏览器暂时不会使用HTTP/3</p>
  </div>
</template>

<script setup></script>
<style scoped>
.danger {
  color: #f56c6c;
}
</style>
