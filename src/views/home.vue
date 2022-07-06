<template>
  <div class="home d-flex justify-center align-center">
    <swiper/>
  </div>

</template>

<script>
import Swiper from '@/components/swiper'
export default {
  name: 'home',
  components: {
    Swiper
  }

}
</script>

<style lang="scss">
.home {
  padding-top: 60px;
  height: 100vh;
  min-height: 600px;
  background: $primary-1;
  @include up($md) {
    padding-top: 80px;
  }


}
</style>
