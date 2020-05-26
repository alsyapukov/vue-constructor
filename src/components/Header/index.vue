<template>
  <header class="header">
    <div class="header__wrap">
      <nav class="nav">
        <div class="nav__item">
          <router-link :to="{ name: 'Main' }">
            Главная
          </router-link>
        </div>
      </nav>
    </div>
  </header>
</template>

<script>

export default {
  data() {
    return {
    };
  }
};
</script>

<style lang="scss" scoped>
.header {
  position: sticky;
  top: 0;
  z-index: 99;
  background: #f6f6f6;
  height: 60px;

  &__wrap {
    display: flex;
    align-items: center;
    height: 100%;
    padding: 0 20px;
  }

  .nav {
    flex-grow: 1;

    &__item {
      cursor: pointer;
    }
  }

  .button {
    &__block {
      display: flex;
    }
    &__item {
      margin-left: 10px;
      &:first-child {
        margin-left: 0;
      }
    }
  }
}
</style>
