<template>
<div>
    <Header></Header>
    <Breadcrumbs></Breadcrumbs>
    <Table></Table>
</div>
</template>

<script>

import Header from '../layouts/Header.vue'
import Breadcrumbs from '../layouts/Breadcrumbs.vue'
import Table from '../components/Table.vue'

export default {
  name: 'PageIndex',
  components: {
    Header,
    Breadcrumbs,
    Table
  }
}
</script>
