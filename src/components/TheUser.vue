<template>
    <div class="user">
      <img :src="imageUrl" alt="" class="user__image">
      <h4 class="user__name">Евгений</h4>
      <h5 class="service__title">Tipping service</h5>
    </div>
</template>

<script>
import imgUrl from './../assets/user.svg';

export default {
  setup() {
    const imageUrl = imgUrl;

    return {
      imageUrl
    }
  }
}
</script>

<style scoped>
.user {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 16px;
}

.user__name {
  font-size: 20px;
  line-height: 24px;
  color: var(--text-color);
  padding-bottom: 6px;
}

.user__image {
  width: 120px;
  height: 120px;
  margin-bottom: 12px;
}

.service__title {
  font-size: 14px;
  line-height: 19px;
  color: var(--gray);
}

</style>
