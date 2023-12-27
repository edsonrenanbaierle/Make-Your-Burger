<template>
  <Banner/>
  <div class="main-container">
    <h1>Monte o seu burger!</h1>
    <Burgerform/>
  </div>
</template>

<script>
import Banner from '@/components/Banner.vue';
import Burgerform from '@/components/Burgerform.vue';
export default {
  name: 'Home',
  components: {
    Banner,
    Burgerform
  }
}
</script>
