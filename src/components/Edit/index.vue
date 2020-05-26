<template>
  <div class="edit">
    <transition-group name="fade" tag="div" v-if="page && page.length">
      <div v-for="(block, i) in page" :key="i" class="edit__block" :ref="`block${i}`">
        <Options class="edit__options" :template="page[i]" :index="i" @remove="blockRemove"/>

        <template v-if="block.type === 'cover'">
          <Cover :template="page[i]"/>
        </template>

        <template v-if="block.type === 'about'">
          <About :template="page[i]"/>
        </template>

        <div class="edit__add" @click="blockAdd(i)">+</div>
      </div>
    </transition-group>
    <div class="edit__create" v-else>
      <Button theme="coral" @click="blockCreate">Создать блок</Button>
    </div>
    <div class="edit__save">
      <Button theme="coral" @click="pageSave">Сохранить</Button>
    </div>
  </div>
</template>

<script>
import Cover from '@/components/Template/Cover'
import About from '@/components/Template/About'
import Options from './Options'
import cover from './templates/cover.json'
import about from './templates/about.json'
import Button from "@/components/base/Button";

export default {
  props: {
    id: {
      type: Number,
      required: true
    }
  },
  components: {
    Options,
    Cover,
    About,
    Button
  },
  data() {
    return {
      cover: {},
      about: {},
      page: [],
      pages: []
    };
  },
  mounted() {
    // конечно нужно шаблоны получать через axios, но я думаю в этой реализации это не обязательно
    this.cover = JSON.parse(JSON.stringify(cover))
    this.about = JSON.parse(JSON.stringify(about))

    this.pages = JSON.parse(this.$localStorage.get('pages'))

    if(!this.pages) {
      this.$localStorage.set('pages', JSON.stringify([[]]))
      this.pages = JSON.parse(this.$localStorage.get('pages'))
    }
    if(this.pages && this.pages[this.id])
      this.page = this.pages[this.id]
  },
  methods: {
    pageSave() {
      this.pages[this.id] = this.page;
      this.$localStorage.set('pages', JSON.stringify(this.pages))
    },
    blockCreate() {
      this.page.push(this.cover)
    },
    blockAdd(i) {
      if(this.page[i].type === 'cover') {
        this.page.splice(i+1, 0, this.about)
      } else {
        this.page.splice(i+1, 0, this.cover)
      }
      this.$nextTick(() => {
        this.blockScrollTo(i+1);
      })
    },
    blockRemove(i) {
      this.page.splice(i, 1)
      this.blockScrollTo(i-1);
    },
    blockScrollTo(i) {
      if(this.$refs[`block${i}`]) {
        this.$refs[`block${i}`][0].scrollIntoView({block: "start", behavior: "smooth"})
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.edit {
  margin: 0 0 200px 0;
  &__block {
    position: relative;
    &::before {
      content: '';
      position: absolute;
      top: 0;
      bottom: 0;
      left: 0;
      right: 0;
      z-index: 1;
      outline-offset: -2px;
      outline: 2px solid #fff;
      outline-style: dashed;
      opacity: 0;
      transition: opacity .3s ease;
    }
    &:hover {
      &::before {
        opacity: 1;
      }
      
      .edit{
        &__options {
          display: block;
        }
        &__add {
          display: flex;
        }
      }
    }
  }

  &__create {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 200px;
  }

  &__save {
    position: fixed;
    bottom: 50px;
    right: 50px;
    z-index: 9;
  }

  &__options {
    display: none;
  }

  &__add {
    position: absolute;
    bottom: 0;
    left: 50%;
    z-index: 9;
    transform: translate(-50%, 50%);

    display: none;
    justify-content: center;
    align-items: center;

    cursor: pointer;
    border-radius: 50%;
    font-size: 30px;
    width: 30px;
    height: 30px;
    background-color: #ff855d;
  }

  .fade-enter-active, .fade-leave-active {
    transition: opacity 1s;
  }
  .fade-enter, .fade-leave-to {
    opacity: 0;
  }
}
</style>
