<template>
  <div id="app">
    <home/>
  </div>
</template>
<script>

import Home from '@/views/home'

export default {
  name: 'App',
  components: {
    Home
  }


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
  overflow: hidden;
  min-width: 320px;
  cursor: default;
  font-family: Avenir, Helvetica, Arial, sans-serif;;
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 20px;
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




a {
  @include transition();
  &:hover {
    opacity: 0.7;
  }
}

p {
  margin-bottom: 0;
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 20px;
  color: $black;
}

label {
  font-size: 10px;
  line-height: 13px;


  letter-spacing: -0.02em;
}


.label-required {
  &::after {
    position: absolute;
    border-radius: 100%;
    content: "";
    top: 0;
    right: -6px;
    width: 4px;
    height: 4px;
    background: $error;
  }
}


h1, h2, h3, h4, h5, h6 {
  margin: 0;
  padding: 0;
  font-weight: 600;
  font-size: 20px;
  line-height: 25px;
}

.d-none {
  display: none !important;
}
.d-block {
  display: block !important;
}

ul {
  margin: 0;
  padding: 0;
  list-style-type: none;
  li {
    margin: 0;
    padding: 0;
  }
}


</style>
