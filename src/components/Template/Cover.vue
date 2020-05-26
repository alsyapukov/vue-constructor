<template>
  <div class="cover">

    <div class="cover__background">
      <img class="background__image" :src="template.background">
    </div>

    <div 
      class="cover__body" 
      :class="{
        center: template.content.position === 'center',
        top: template.content.position === 'top',
        bottom: template.content.position === 'bottom'
      }"
    >
      <div class="cover__content" :class="{ reverse: template.content.reverse }">
        <h1 
          class="cover__title" 
          :style="{
            'font-size': template.content.title.size,
            color: template.content.title.color
          }"
        >{{ template.content.title.text }}</h1>
        <p 
          class="cover__description"
          :style="{
            'font-size': template.content.description.size,
            'line-height': template.content.description.interval,
            color: template.content.description.color,
            'margin-top': template.content.description.top
          }"
        >{{ template.content.description.text }}</p>
      </div>
    </div>

  </div>
</template>

<script>

export default {
  name: "Cover",
  props: {
    template: {
      type: Object,
      default: {}
    }
  },
  components: {
  },
  data() {
    return {
    };
  }
};
</script>

<style lang="scss" scoped>
.cover {
  position: relative;
  height: 100vh;

  &__body {
    position: relative;
    z-index: 1;

    display: flex;
    justify-content: center;

    height: 100%;
    padding: 60px 30px;

    &.top {
      align-items: flex-start;
    }
    &.center {
      align-items: center;
    }
    &.bottom {
      align-items: flex-end;
    }
  }

  &__content {
    display: flex;
    flex-direction: column;
    max-width: 1000px;

    &.reverse {
      flex-direction: column-reverse;
    }
  }

  &__title {
    text-align: center;
    text-transform: uppercase;
  }
  &__description {
    margin-top: 20px;
    text-align: center;
  }





  &__background {
    position: absolute;
    width: 100%;
    height: 100%;
    &::before {
      content: '';
      background-image: -webkit-linear-gradient(top, rgba(0,0,0,0.70), rgba(0,0,0,0.70));
      position: absolute;
      top: 0;
      bottom: 0;
      left: 0;
      right: 0;
    }
  }

  .background {
    &__image {
      object-fit: cover;
      width: 100%;
      height: 100%;
    }
  }
}
</style>
