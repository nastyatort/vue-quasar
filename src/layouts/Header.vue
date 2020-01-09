<template>
  <div class="header-wrapper">
      <q-layout view="lHh lpr lFf" container>
        <q-header class="header">
          <Navigations></Navigations>
          <Breadcrumbs></Breadcrumbs>
        </q-header>
      </q-layout>
    </div>
</template>

<script>

import Breadcrumbs from './Breadcrumbs.vue'
import Navigations from './Navigations.vue'

export default {
  name: 'Header',
  components: {
    Breadcrumbs,
    Navigations
  },
  data () {
    return {
    }
  },
  methods: {}
}
</script>
