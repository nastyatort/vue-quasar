<template>
      <div class="header-wrapper">
      <div class="container">
    <q-layout view="lHh lpr lFf" container>
      <q-header class="header">
        <div class="header-content row justify-between items-center">
        <q-tabs
        v-model="tab"
        align="left"
        >
          <q-route-tab to="/" name="name1" label="home" />
          <q-route-tab to="/other" name="name2" label="Cadastro do salão" />
          <q-route-tab to="/other" name="name3" label="Cadastro de parceiros" />
          <q-route-tab to="/other" name="name4" label="Visualizar NFSe" />
          <q-route-tab to="/other" name="name5" label="Visualizar DAS" />
        </q-tabs>
        <div class="user justify-between items-center row">
            <div class="user-info justify-between items-center row">
                <q-avatar class="user-avatar" size="36px" font-size="36px">
                <img v-bind:src="'statics/icons/' + avatar" />
                </q-avatar>
                <div class="user-name">
                    <p>Ola,</p>
                    <p class="user-name">{{user}}!</p>
                </div>
            </div>
        <q-btn id="logout" label="sair" unelevated icon="img:statics/icons/logout.png" />
        </div>
        </div>
      </q-header>
    </q-layout>
      </div>
      </div>
</template>

<script>
export default {
  name: 'Header',
  data () {
    return {
      tab: 'name4',
      user: 'SalÃo Dany',
      avatar: 'user.png'
    }
  },
  methods: {
  }
}
</script>
