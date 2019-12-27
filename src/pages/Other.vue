<template>
<div>
    <Header></Header>
    <Breadcrumbs></Breadcrumbs>
    <div class="container">
    <div>other pages</div>
    </div>
</div>
</template>

<script>

import Header from '../layouts/Header.vue'
import Breadcrumbs from '../layouts/Breadcrumbs.vue'

export default {
  name: 'Other',
  components: {
    Header,
    Breadcrumbs
  }
}
</script>
