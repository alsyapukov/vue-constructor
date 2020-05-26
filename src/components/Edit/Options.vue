<template>
  <div class="options">
    <div class="options__wrap">
      <div class="options__button" @click="settingsClick">
        <span>Настройки</span>
      </div>
      <div class="options__button" @click="$emit('remove', index)" v-if="settingsRemoveShow">
        <span>Удалить блок</span>
      </div>
      <transition name="fade" v-if="Object.keys(settings).length">
        <div class="settings" v-show="settingsShow">
          <div class="settings__item">
            <div class="settings__title">Фоновое изображение</div>
            <div class="settings__control">
              <TextBox v-model="settings.background" placeholder="Укажите ссылку" />
            </div>
          </div>
          <div class="settings__item">
            <div class="settings__title">Позиция контента</div>
            <div class="settings__control">
              <label>
                <input type="radio" :name="`position${index}`" v-model="settings.content.position" value="top" />
                <span>Сверху</span>
              </label>
              <label>
                <input type="radio" :name="`position${index}`" v-model="settings.content.position" value="center" />
                <span>В центре</span>
              </label>
              <label>
                <input type="radio" :name="`position${index}`" v-model="settings.content.position" value="bottom" />
                <span>Снизу</span>
              </label>
            </div>
          </div>
          <div class="settings__item">
            <div class="settings__title">Заголовок/описание (поменять местами)</div>
            <div class="settings__control">
              <label>
                <input type="radio" :name="`reverse${index}`" v-model="settings.content.reverse" :value="false" />
                <span>Сверху/снизу</span>
              </label>
              <label>
                <input type="radio" :name="`reverse${index}`" v-model="settings.content.reverse" :value="true" />
                <span>Снизу/сверху</span>
              </label>
            </div>
          </div>

          <!-- * Title * -->
          <div class="settings__item">
            <div class="settings__title">Текст заголовка</div>
            <div class="settings__control">
              <TextBox v-model="settings.content.title.text" placeholder="Введите заголовок" />
            </div>
          </div>
          <div class="settings__item">
            <div class="settings__title">Цвет заголовка</div>
            <div class="settings__control">
              <TextBox v-model="settings.content.title.color" placeholder="Укажите цвет заголовка" />
            </div>
          </div>
          <div class="settings__item">
            <div class="settings__title">Размер заголовка</div>
            <div class="settings__control">
              <TextBox v-model="settings.content.title.size" placeholder="Размер заголовка" />
            </div>
          </div>

          <!-- * Description * -->
          <div class="settings__item">
            <div class="settings__title">Текст описания</div>
            <div class="settings__control">
              <TextBox v-model="settings.content.description.text" placeholder="Введите описания" />
            </div>
          </div>
          <div class="settings__item">
            <div class="settings__title">Цвет описания</div>
            <div class="settings__control">
              <TextBox v-model="settings.content.description.color" placeholder="Укажите цвет описания" />
            </div>
          </div>
          <div class="settings__item">
            <div class="settings__title">Размер описания</div>
            <div class="settings__control">
              <TextBox v-model="settings.content.description.size" placeholder="Размер описания" />
            </div>
          </div>
          <div class="settings__item">
            <div class="settings__title">Отступ между названием и описанием</div>
            <div class="settings__control">
              <TextBox v-model="settings.content.description.top" placeholder="Укажите отступ" />
            </div>
          </div>
          <div class="settings__item">
            <div class="settings__title">Межстрочный интервал описания</div>
            <div class="settings__control">
              <TextBox v-model="settings.content.description.top" placeholder="Укажите межстрочный интервал" />
            </div>
          </div>

          <!-- * Button * -->
          <template v-if="settings.content.button">
            <div class="settings__item">
              <div class="settings__title">Текст кнопки</div>
              <div class="settings__control">
                <TextBox v-model="settings.content.button.text" placeholder="Введите текст кнопки" />
              </div>
            </div>
            <div class="settings__item">
              <div class="settings__title">Цвет текста кнопки</div>
              <div class="settings__control">
                <TextBox v-model="settings.content.button.color" placeholder="Укажите цвет текста кнопки" />
              </div>
            </div>
            <div class="settings__item">
              <div class="settings__title">Цвет кнопки</div>
              <div class="settings__control">
                <TextBox v-model="settings.content.button.background" placeholder="Укажите цвет кнопки" />
              </div>
            </div>
            <div class="settings__item">
              <div class="settings__title">Размер кнопки</div>
              <div class="settings__control">
                <TextBox v-model="settings.content.button.size" placeholder="Размер кнопки" />
              </div>
            </div>
            <div class="settings__item">
              <div class="settings__title">Отступ между описанием и кнопкой</div>
              <div class="settings__control">
                <TextBox v-model="settings.content.button.top" placeholder="Укажите отступ" />
              </div>
            </div>
          </template>
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
import TextBox from "@/components/base/TextBox";

export default {
  name: "Options",
  props: {
    template: {
      type: Object,
      default: {}
    },
    index: {
      type: Number,
      required: true
    }
  },
  components: {
    TextBox
  },
  data() {
    return {
      settingsShow: false,
      settingsRemoveShow: false,
      settings: {}
    };
  },
  mounted() {
    this.settings = this.template;
  },
  methods: {
    settingsClick() {
      this.settingsShow = !this.settingsShow;
      this.settingsRemoveShow = !this.settingsRemoveShow;
    }
  }
};
</script>

<style lang="scss" scoped>
.options {
  position: absolute;
  top: 20px;
  left: 20px;
  z-index: 9;

  &__wrap {
    position: relative;
    display: flex;
  }

  &__button {
    background-color: #ff855d;
    z-index: 2;
    padding: 10px;
    border-radius: 4px;
    cursor: pointer;
    box-shadow: 0px 0px 4px rgba(0, 0, 0, 0.2);
    margin-right: 10px;
  }
  .settings {
    position: absolute;
    top: calc(100% + 10px);
    left: 0;
    width: 300px;
    padding: 20px;
    background-color: #fff;
    box-shadow: 0px 0px 14px rgba(0, 0, 0, 0.1);
    max-height: 500px;
    overflow: auto;

    &__item {
      margin-bottom: 20px;
      &:last-child {
        margin-bottom: 0;
      }
    }
    &__control {
      margin-top: 10px;
    }
  }
  .fade-enter-active, .fade-leave-active {
    transition: opacity .3s;
  }
  .fade-enter, .fade-leave-to {
    opacity: 0;
  }
}
</style>
