<template>
  <div class="add-product-form" :class="active? 'add-product-form__active': ''">
    <a v-show="!active" class="add-product-form__burger" @click="active = !active">
      <span></span>
      <span></span>
      <span></span>
    </a>
    <div>
      <h2>Добавление товара</h2>
      <img v-show="active" @click="active = !active" src="@/assets/close.svg" alt="Img">
      <form @submit.prevent="onSubmit">
        <div>
          <label for="name" class="label-required">Наименование товара</label>
          <input v-model="form.name" type="text" id="name" required placeholder="Введите наименование товара">
          <span v-show="nameError">{{ nameError }}</span>
        </div>

        <div>
          <label for="description">Описание товара</label>
          <input v-model="form.description" type="text" id="description" placeholder="Введите описание товара">
        </div>

        <div>
          <label for="link" class="label-required">Ссылка на изображение товара</label>
          <input v-model="form.url" type="text" id="link" required placeholder="Введите ссылку">
          <span v-show="urlError">{{ urlError }}</span>
        </div>

        <div>
          <label for="price" class="label-required">Цена товара</label>
          <input v-model="form.price" type="text" id="price" required placeholder="Введите цену">
          <span v-show="priceError">{{ priceError }}</span>
        </div>

        <button :disabled="disabled" :class="{'disabled': disabled}" type="submit">Добавить товар</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "add-product-from",
  data() {
    return {
      active: false,
      disabled: true,

      nameReg: /^$|[a-zA-Zа-яА-Я]+$/,
      urlReg: /^$|(http[s]?:\/\/.*\.(?:png|jpg|svg|jpeg))/i,
      priceReg: /^$|[\d\.,]+$/,

      form: {
        name: '',
        description: '',
        price: '',
        url: ''
      }
    }
  },
  watch: {
    form: {
      handler(newValue) {
        //Name check
        console.log(this.disabled)
        if (!this.isError) {
          if (newValue.name && newValue.url && newValue.price) {
            this.disabled = false;
          }
        } else {
          this.disabled = true;
        }
      },
      deep: true,
    }
  },
  computed: {
    nameError() {
      return RegExp(this.nameReg).test(this.form.name) ? "" : "Введите правильное имя";
    },
    urlError() {
      return RegExp(this.urlReg).test(this.form.url) ? "" : "Введите правильную ссылку";
    },
    priceError() {
      return RegExp(this.priceReg).test(this.form.price) ? "" : "Введите правильную цену";
    },
    isError() {
      return (Boolean(this.nameError) || Boolean(this.urlError) || Boolean(this.priceError))
    }
  },
  methods: {
    onSubmit() {

      this.$emit('submit', this.form)

      this.active = false;
      this.disabled = true;
      this.form = {
        name: '',
        description: '',
        price: '',
        url: ''
      }
    }
  }

}
</script>

<style lang="scss">
.add-product-form {
  position: absolute;
  width: 0;


  @include up($md) {
    width: 30%;
    position: static;
  }

  & > div {
    position: relative;
    display: none;
    @include up($md) {
      display: block;
    }
  }

  &__active {
    z-index: 10;
    @include transition();
    min-width: 320px;
    box-sizing: border-box;
    background-color: rgba(0, 0, 0, 0.4);
    width: 100%;
    height: 100%;
    position: absolute;
    display: flex;
    align-items: center;
    justify-content: center;
    top: 0;
    margin: 0 -12px;
    padding: 20px;
    @include up($sm) {
      margin: 0 -32px;
    }


    & > div {

      display: block;
    }
  }

  h2 {
    position: absolute;
    left: 24px;
    top: 30px;
    @include up($md) {

      top: -16px;
      left: 0;
      line-height: 0;
    }
  }

  img {
    cursor: pointer;
    width: 20px;
    height: 20px;
    position: absolute;
    top: 32px;
    right: 24px;
    @include transition();

    &:hover {
      opacity: 0.7;
    }
  }

  form {
    background: $white;
    padding: 60px 24px 24px;
    box-sizing: border-box;
    box-shadow: 0 20px 30px rgba(0, 0, 0, 0.04), 0 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;

    @include up($md) {
      padding: 24px;
    }

    & > div {
      margin-bottom: 16px;
    }
    input {
      box-sizing: border-box;
      width: 100%;

      padding: 10px 16px;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
      border-radius: 4px;
      border: none;


      &::placeholder {
        font-size: 12px;
        line-height: 15px;
        color: $grey;
      }
    }

    label {
      position: relative;
      margin-bottom: 4px;


    }

    span {
      font-size: 8px;
      line-height: 10px;
      margin: 4px 0;
      color: $error;
    }

    button {
      cursor: pointer;
      width: 100%;
      height: 36px;
      display: flex;
      align-items: center;
      justify-content: center;
      border: none;
      border-radius: 10px;
      background: $green;
      color: $white;
      font-weight: 600;
      font-size: 12px;
      letter-spacing: -0.02em;

      &.disabled {
        cursor: default;
        background: $light-grey;
        color: $grey;
      }
    }
  }

  &__burger {
    position: absolute;
    cursor: pointer;
    top: -40px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;

    width: 20px;
    height: 20px;
    @include up($md) {
      display: none;
    }

    span {
      width: 100%;
      height: 2px;
      background: $black;
      @include transition();

      &:nth-child(2) {
        width: 15px;
      }
    }

    &:hover {
      span {
        &:nth-child(1n) {
          width: 15px;
        }

        &:nth-child(2) {
          width: 100%;
        }
      }

    }
  }


}
</style>
