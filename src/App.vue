<template>
  <main role="main">
    <Header />
    <User />
    <PaymentForm />
  </main>
</template>

<script>
import Header from './components/TheHeader.vue'
import User from './components/TheUser.vue'
import PaymentForm from './components/payment-form.vue'

export default {
  components: {
    Header,
    User,
    PaymentForm
  }
}
</script>

<style>
@import "main.scss";
</style>
