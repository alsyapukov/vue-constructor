<template>
  <div class="page">
    <Header />
    <Edit :id="Number(id)"/>
  </div>
</template>

<script>
import Header from '@/components/Header/'
import Edit from '@/components/Edit'

export default {
  props: {
    id: {
      required: true
    }
  },
  components: {
    Header,
    Edit
  }
}
</script>

<style lang="scss" scoped></style>
