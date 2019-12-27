<template>
<div class="breadcrumbs-wrapper">
    <div class="container">
        <div class="breadcrumbs">
    <q-breadcrumbs>
      <q-breadcrumbs-el icon="img:statics/icons/home.png" to="/" />
      <q-breadcrumbs-el label="pageIndex" to="/pageIndex"/>
      <q-breadcrumbs-el label="other" to="/other" />
    </q-breadcrumbs>
        </div>
    </div>
</div>
</template>

<script>
export default {
  name: 'Breadcrumbs',
  data () {
    return {
    }
  },
  methods: {
  }
}
</script>
