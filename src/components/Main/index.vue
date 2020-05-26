<template>
  <div class="main">
    <div class="site">
      <ul class="site__list" v-if="sites && sites.length">
        <li class="site__item" v-for="(site, i) in sites" :key="i">
          <div class="site__block">
            <div class="site__head">{{ `Сайт ${i}` }}</div>
            <div class="site__panel">
              <router-link class="site__edit" :to="{ name: 'Edit', params: {id: i} }">Редактирование</router-link>
              <router-link
                class="site__preview"
                :to="{ name: 'Preview', params: {id: i} }"
              >Предпросмотр</router-link>
            </div>
          </div>
        </li>
      </ul>
      <p v-else>У вас пока нет сайтов, но вы можете его создать!</p>
    </div>
    <div class="create-site">
      <Button theme="coral" @click="createSite">Создать сайт</Button>
    </div>
  </div>
</template>

<script>
import Button from "@/components/base/Button";

export default {
  components: {
    Button
  },
  data() {
    return {
      sites: []
    };
  },
  mounted() {
    this.sites = JSON.parse(this.$localStorage.get("pages"));
  },
  methods: {
    createSite() {
      if(this.sites)
        this.sites.push([]);
      else
        this.sites = [[]];
        
      this.$localStorage.set('pages', JSON.stringify(this.sites))

      this.$router.push({
        name: 'Edit',
        params: {
          id: this.sites.length - 1
        }
      })
    }
  }
};
</script>

<style lang="scss" scoped>
.main {
  .create-site {
    position: fixed;
    bottom: 50px;
    right: 50px;
  }

  .site {
    display: flex;
    justify-content: center;
    width: 100%;
    height: 100%;
    margin: 100px 0;
    &__list {
      display: flex;
      flex-direction: column;
      align-items: center;
      width: 300px;
    }
    &__block {
      margin-bottom: 20px;
    }
    &__head {
      border-top: 1px solid #000;
      border-left: 1px solid #000;
      border-right: 1px solid #000;
      padding: 20px;
      font-size: 20px;
    }
    &__panel {
      display: flex;
      height: 100px;

      a {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100%;
        padding: 20px;
        border-top: 1px solid #000;
        border-bottom: 1px solid #000;
        border-right: 1px solid #000;
        font-size: 18px;
        width: 50%;
        &:hover {
          opacity: 0.9;
        }
      }
    }
    &__edit {
      border-left: 1px solid #000;
      background: #ff855d;
    }
    &__preview {
      color: #fff;
      background: #000;
    }
  }
}
</style>
