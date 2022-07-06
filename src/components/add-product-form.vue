<template>
  <div class="add-product-from">
    <h2>Добавление товара</h2>
    <form action="#">
      <input type="text" placeholder="Введите наименование товара">

    </form>
  </div>
</template>

<script>
export default {
  name: "add-product-from"
}
</script>

<style lang="scss">
.add-product-from {

  form {
    background: $white;
    padding: 24px;
    width: 332px;
  }
}
</style>
