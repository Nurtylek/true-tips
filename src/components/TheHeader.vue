<template>
  <header class="header">
    <img :src="imgUrl" alt="">
  </header>
</template>

<script>
import imgUrl from './../assets/logo.svg';
export default {
  setup() {
    const imageUrl = imgUrl;

    return {
      imgUrl: imageUrl
    }
  }
}
</script>

<style scoped>
.header {
  display: flex;
  align-items: center;
  justify-content: flex-end;

  padding-right: 15px;
  padding-left: 15px;
  padding-top: 30px;
  /*width: 1170px;*/
  margin: 0 auto;
}
</style>
