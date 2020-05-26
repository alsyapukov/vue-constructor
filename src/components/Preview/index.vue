<template>
  <div class="preview">
    <transition-group name="fade" tag="div" v-if="page.length">
      <div v-for="(block, i) in page" :key="i" class="preview__block" :ref="`block${i}`">

        <template v-if="block.type === 'cover'">
          <Cover :template="page[i]"/>
        </template>

        <template v-if="block.type === 'about'">
          <About :template="page[i]"/>
        </template>
      </div>
    </transition-group>
  </div>
</template>

<script>
import Cover from '@/components/Template/Cover'
import About from '@/components/Template/About'

export default {
  props: {
    id: {
      type: Number,
      required: true
    }
  },
  components: {
    Cover,
    About
  },
  data() {
    return {
      page: [],
    };
  },
  mounted() {
    this.page = JSON.parse(this.$localStorage.get('pages'))[this.id]
  }
};
</script>

<style lang="scss" scoped>
.preview {
  margin: 0 0 200px 0;
  &__block {
    position: relative;
  }
  .fade-enter-active, .fade-leave-active {
    transition: opacity 1s;
  }
  .fade-enter, .fade-leave-to {
    opacity: 0;
  }
}
</style>
