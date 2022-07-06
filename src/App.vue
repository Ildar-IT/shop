<template>
  <v-app>
    <transition name="route" mode="out-in">
      <router-view/>
    </transition>
  </v-app>
</template>
<script>

export default {
  name: 'App',

  data: () => ({
    //
  }),
};
</script>

<style lang="scss">
:root {
  --vh: 1vh;
  --gray: #B3B8CB;
}




html {
  overflow-y: inherit;
  overflow-x: hidden;
}

body {
  box-sizing: border-box;
  cursor: default;
  font-family: Avenir, Helvetica, Arial, sans-serif;;
  font-weight: 300;
  font-style: normal;
  font-size: 13px;
  line-height: 27px;
  padding: 0;
  margin: 0;
  color: $black;
  @include up($md) {
    font-size: 18px;
  }
  @include up($lg) {
    font-size: 24px;
  }
}
#app {
  overflow: hidden;
  min-width: 320px;

  p {
    margin-bottom: 0;

  }
}
a {
  @include transition();
  &:hover {
    opacity: 0.7;
  }
}



</style>
