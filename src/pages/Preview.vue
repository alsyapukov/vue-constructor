<template>
  <div class="page">
    <Header />
    <Preview :id="Number(id)"/>
  </div>
</template>

<script>
import Header from '@/components/Header/'
import Preview from '@/components/Preview'

export default {
  props: {
    id: {
      required: true
    }
  },
  components: {
    Header,
    Preview
  }
}
</script>

<style lang="scss" scoped></style>
