<template>
  <div class="form__container">
    <form class="form">
      <div class="form__group">
        <input class="input" placeholder="2500 тг." type="text" >
        <img :src="imgUrl" alt="" class="input__clear">
      </div>
      <StarRating @onRatingSelected="selectRating"/>

      <div class=feedback>
        <span class="feedback__title" v-if="rating">В чем мы можем стать лучше?</span>
        <template v-if="rating < 4 && rating !== null">
          <div class="items">
            <label class="item" v-for="f in feedback" :key="f">
              <span :for="f.id">{{ f.name }}</span>
              <input type="checkbox" :id="f.id" v-model="selectedFeedBack" :value="f">
            </label>
          </div>
        </template>
        <template v-if="rating >= 4 && rating !== null">
          <div class="good">
            <label :for="g.id" class="good__item" v-for="g in goods" :key="g">
              <img :src="g.url" :alt="g.name">
              <span :class="{ active: activeGood(g.id) }">{{ g.name }}</span>
              <input type="checkbox" class="good__input" :id="g.id" v-model="selectedGood" :value="g">
            </label>
          </div>
        </template>
      </div>
      <textarea placeholder="Расскажите подробнее...(необязательно)" v-model="comment" class="comment"></textarea>
      <div class="pay__wrapper">
        <button class="pay" @click="$event.preventDefault()">Оплатить картой</button>
      </div>
      <div class="policy">
        <label for="1">
          <input type="checkbox" id="1">
          <span>Я хочу взять на себя транзакционные издержки (122 т.), чтобы сотрудник получил полную сумму</span>
        </label>
        <label for="2">
          <input type="checkbox" id="2">
          <span>Согласен с условиями <span class="highlight">Пользовательского соглашения</span> и <span class="highlight">Политики обработки персональных данных</span></span>
        </label>
      </div>
    </form>
  </div>
</template>

<script>
import clear from './../assets/clear.svg';

import good1 from './../assets/good-1.svg'
import good2 from './../assets/good-2.svg'
import good3 from './../assets/good-3.svg'
import good4 from './../assets/good-4.svg'

import StarRating from '../components/star-rating.vue'

export default {
  components: {
    StarRating
  },
  data: () => {
    return {
      comment: '',
      imgUrl: clear,
      rating: null,
      feedback: [
        {
          id: 1,
          name: 'Обслуживание'
        },
        {
          id: 2,
          name: 'Чистота'
        },
        {
          id: 3,
          name: 'Атмосфера'
        },
        {
          id: 4,
          name: 'Качество блюд'
        }
      ],
      selectedFeedBack: [],
      goods: [
        {
          id: 1,
          name: 'Чисто',
          url: good1
        },
        {
          id: 2,
          name: 'Вкусная еда',
          url: good2
        },
        {
          id: 3,
          name: 'Хорошее обслуживание',
          url: good3
        },
        {
          id: 4,
          name: 'Приятная атмосфера',
          url: good4
        }
      ],
      selectedGood: []
    }
  },
  methods: {
    selectRating(rating) {
      this.rating = rating;
    },
    activeGood(id) {
      return !!this.selectedGood.find(g => g.id === id)
    }
  },
  watch: {
    rating(val) {
      if (val >= 4) {
        this.selectedGood = [];
      } else {
        this.selectedFeedBack = []
      }
    }
  }
}
</script>

<style scoped>
.form__container {
  background-color: var(--form-bg-color);
  box-shadow: 0 6px 24px rgba(25, 1, 52, 0.1);
  border-radius: 15px;
  padding: 12px;
  margin: 24px 15px;
}

.form__group {
  position: relative;
}

.input {
  background-color: transparent;
  border: none;
  border-bottom: 1px solid var(--primary-green);
  padding: 16px 0;
  font-family: inherit;
  width: 100%;
  font-size: 20px;
  color: var(--text-color);
}

.input::placeholder {
  color: var(--text-color);
}

.input__clear {
  position: absolute;
  right: 0;
  top: 14px;
}

.input:focus {
  outline: none;
}

input::-webkit-input-placeholder {
  color: #AAA;
}

.feedback {
  margin-top: 24px;
}

.feedback__title {
  display: block;
  font-size: 14px;
  line-height: 17px;
  text-align: center;
  color: var(--gray);
  margin-bottom: 20px;
}

.items {
  display: flex;
  flex-direction: column;
}

.item {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.item + .item {
  padding-top: 16px;
}

label {
  font-size: 16px;
  line-height: 19px;
}

@supports (-webkit-appearance: none) or (-moz-appearance: none) {
  input[type="checkbox"] {
    height: 20px;
    width: 20px;
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
    outline: none;
    transition-duration: 0.1s;
    cursor: pointer;
    background: var(--form-bg-color);
    border-radius: 4px;
    margin: 0;
    padding: 0;
    border: 1px solid var(--gray);
  }

  input:checked {
    background-size: 14px 14px;
    background: var(--primary-green) url('./../assets/check.svg') no-repeat center;
  }
}

.good {
  display: flex;
  align-items: center;
  justify-content: space-evenly;
  gap: 2px;
}

.good > * {
  flex-basis: 100%;
}

.good__item {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.good__item img {
  margin-bottom: 16px;
  width: 65px;
  height: 65px;
}

.good__input {
  visibility: hidden;
  width: 0;
  height: 0;
}

.active {
  color: var(--primary-green);
}

.comment {
  border: 1px solid #FFFFFF;
  border-radius: 5px;
  width: 100%;
  background: inherit;
  padding: 12px;
  color: var(--text-color);
  font-size: 14px;
  line-height: 17px;
  margin-top: 16px;
}

.comment:focus {
  outline: none;
}

.pay__wrapper {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.pay {
  font-family: inherit;
  background: var(--primary-green);
  box-shadow: 0 6px 20px rgba(32, 178, 93, 0.4);
  border-radius: 10px;
  padding: 12px;
  color: var(--text-color);
  border: none;
  margin-top: 16px;
}

.pay:focus {
  outline: none;
}

.policy {
  margin-top: 25px;
  display: grid;
  gap: 16px;
}

.policy label {
  display: grid;
  grid-template-columns: 10% 90%;
  align-items: center;
}

.policy label span {
  color: var(--gray);
}

.highlight {
  text-decoration: underline;
}
</style>
