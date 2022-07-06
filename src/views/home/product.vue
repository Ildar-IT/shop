<template>
  <section class="product">
    <span class="product__delete" @click="deleteItem(item.id)">
      <img  src="@/assets/delete.svg" alt="Delete">
    </span>
    <img :src="item.url" alt="Img">
    <div>
      <h5>{{ item.name }}</h5>
      <p>{{ item.description }}</p>
      <span>{{ item.price.toLocaleString() }} руб.</span>
    </div>
  </section>
</template>

<script>
export default {
  name: "product",
  props:['item'],
  methods: {
    deleteItem(id) {
      this.$emit('delete', id)
    }
  }
}
</script>

<style lang="scss">
.product {
  position: relative;
  cursor: pointer;
  background-color: $white;
  box-sizing: border-box;
  box-shadow: 0 20px 30px rgba(0, 0, 0, 0.04), 0 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  width: 100%;
  margin-bottom: 32px;
  padding: 8px ;
  @include transition();
  &:hover {
    opacity: 0.7;
  }
  @include up($sm) {
    margin: 0 16px 16px 0;
    width: calc((100% / 2) - 16px);
  }

  @include up($md) {
    width: calc((100% / 3) - 16px);
  }
  div {
    min-height: 215px;
    padding: 0 16px 24px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }

  &__delete {
    position: absolute;
    z-index: 2;
    top: 0;
    right: 0;
    width: 32px;
    height: 32px;
    background: $error;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    @include transition();

    img {
      width: 16px;
      height: 16px;
    }
    &:hover {
      background: $light-black;
      img {
        opacity: 0.7;
      }
    }
  }

  & > img {
    width: 100%;
    min-height: 270px;
    height: 270px;
    object-fit: cover;
    border-radius: 4px 4px 0 0;
    @include up($sm) {
      min-height: 200px;
      height: 200px;
    }
  }
  h5 {
    margin:  16px 0;
  }
  p {
    margin-bottom: 32px;
  }
  span {
    font-weight: 600;
    font-size: 24px;
    line-height: 30px;

    color: $black;
  }
}
</style>
