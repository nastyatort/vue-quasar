<template>
  <div class="breadcrumbs-wrapper">
    <div class="container">
      <div class="breadcrumbs">
        <q-breadcrumbs>
          <q-breadcrumbs-el icon="img:statics/icons/home.png" to="/"></q-breadcrumbs-el>
          <q-breadcrumbs-el
            v-for="(item) in breadcrumbs"
            :key="item.label"
            :to="item.to"
            :label="item.label"
          />
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
      breadcrumbs: [
        {
          label: 'other',
          to: '/other'
        },
        {
          label: 'pageIndex',
          to: '/pageIndex'
        }
      ]
    }
  },
  methods: {}
}
</script>
