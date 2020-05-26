<template>
  <div class="about" :style="{ 'background-color': template.background }">
    <div 
      class="about__body"
      :class="{
        center: template.content.position === 'center',
        top: template.content.position === 'top',
        bottom: template.content.position === 'bottom'
      }"
    >
      <div class="about__content" :class="{ reverse: template.content.reverse }">
        <h1 
          class="about__title" 
          :style="{
            'font-size': template.content.title.size,
            color: template.content.title.color
          }"
        >{{ template.content.title.text }}</h1>
        <p 
          class="about__description"
          :style="{
            'font-size': template.content.description.size,
            'line-height': template.content.description.interval,
            color: template.content.description.color,
            'margin-top': template.content.description.top
          }"
        >{{ template.content.description.text }}</p>
        <div class="about__button">
          <button 
            class="button"
            :style="{
              'font-size': template.content.button.size,
              color: template.content.button.color,
              'margin-top': template.content.button.top,
              'background-color': template.content.button.background
            }"
          >{{ template.content.button.text }}</button>
        </div>
      </div>
    </div>

  </div>
</template>

<script>

export default {
  name: "About",
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
.about {
  position: relative;
  height: 600px;

  &__body {
    position: relative;
    z-index: 1;

    display: flex;
    justify-content: center;
    padding: 40px 30px;
    height: 100%;

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
  &__button {
    display: flex;
    justify-content: center;

    .button {
      outline: none;
      cursor: pointer;
      border: none;
      border-radius: 30px;
      padding: 16px 30px;
    }
  }
}
</style>
