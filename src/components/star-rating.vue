<template>
  <div class="star-rating">
    <span class="star-rating__hint">Вам всe понравилось?</span>
    <star-rating
        active-color="#20B25D"
        :show-rating="false"
        v-model:rating="rating"
        :star-size="50"
        :rounded-corners="false"
        :border-width="0"
        :star-points="[23,2, 14,17, 0,19, 10,34, 7,50, 23,43, 38,50, 36,34, 46,19, 31,17]"
    />
  </div>
</template>

<script>
import StarRating from 'vue-star-rating';
export default {
  components: {
    StarRating
  },
  data: () => {
    return {
      rating: null
    }
  },
  emits: ['onRatingSelected'],
  watch: {
    rating(value) {
      this.$emit('onRatingSelected', value)
    }
  }
}
</script>

<style scoped>

.star-rating {
  padding-top: 30px;
  text-align: center;
}

.star-rating__hint {
  color: var(--gray);
  font-size: 14px;
  line-height: 17px;
  margin-bottom: 16px;
  display: block;
}
</style>
