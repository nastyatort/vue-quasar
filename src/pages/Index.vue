<template>
  <div>
    <Header></Header>
    <Filters></Filters>
  </div>
</template>

<script>
import Header from '../layouts/Header.vue'
import Filters from '../components/Filters.vue'

export default {
  name: 'PageIndex',
  components: {
    Header,
    Filters
  }
}
</script>
