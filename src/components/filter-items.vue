<template>
  <div v-if="selectList.length >= 1"
       class="filter-items"
       :class="{'filter-items-active':active}"
       @click="openPopup">

        <span class="filter-items-item " :class="{'filter-items-item-active':active}">
          {{ activeSelectName }}
        </span>
    <ul :class="active ? 'd-block':'d-none'">
      <li v-for="item in selectList" :key="item.id" @click.stop="selectItem(item.name, item.id)">
        {{ item.name }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "filter-items",
  data() {
    return {
      active: null,
      activeSelectName: 'По умолчанию',
      selectList: [
        {id: '1', name: 'По умолчанию'},
        {id: '2', name: 'По наименованию'},
        {id: '3', name: 'По возрастанию цены'},
        {id: '4', name: 'По уменьшению цены'},
      ],
    }
  },
  methods: {
    openPopup() {
      this.active = true;
    },
    selectItem(name, id) {
      this.active = false;
      this.activeSelectName = name;

      this.$emit('selectID', id)
    }
  }
}
</script>

<style lang="scss">
.filter-items {
  z-index: 10;
  font-style: normal;
  font-weight: 400;
  font-size: 12px;
  line-height: 15px;
  color: $grey;

  cursor: pointer;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 16px 10px;
  position: absolute;
  top: 31px;
  right: 12px;
  width: 150px;
  background: $white;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  @include transition();

  &:hover {
    opacity: 0.7;
  }

  &-active {
    &:hover {
      opacity: 1;
    }
  }

  @include up($sm) {

    right: 48px;
  }

  &-item {
    position: relative;


    &::after {
      z-index: 1;
      position: absolute;
      content: "";
      background-image: url("~@/assets/arr-down.svg");
      background-size: cover;
      width: 10px;
      height: 5px;
      top: 5px;
      right: 11px;
      @include transition-long();
    }

    &-active {
      &::after {
        transform: rotate(180deg);
      }
    }
  }

  ul {
    margin-top: 14px;

    li {
      margin-bottom: 4px;

      &:hover {
        color: $light-black;
      }
    }
  }

}


</style>
