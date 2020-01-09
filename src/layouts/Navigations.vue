<template>
  <div class="navigations-wrapper">
    <div class="container">
        <div class="navigations">
          <div class="navigations-content row justify-between items-center">
            <q-tabs align="left">
              <q-route-tab
                v-for="(item) in nav"
                :key="item.name"
                :to="item.to"
                :name="item.name"
              >{{item.lable}}</q-route-tab>
            </q-tabs>
            <div class="user justify-between items-center row">
              <div class="user-info justify-between items-center row">
                <q-avatar class="user-avatar" size="36px" font-size="36px">
                  <img :src="`statics/icons/${avatar}`" />
                </q-avatar>
                <div class="user-name">
                  <p>Ola,</p>
                  <p class="user-name">{{user}}!</p>
                </div>
              </div>
              <q-btn id="logout" class="logout" label="sair" unelevated icon="img:statics/icons/logout.png" />
            </div>
          </div>
        </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Navigations',
  data () {
    return {
      user: 'SalÃo Dany',
      avatar: 'user.png',
      nav: [
        {
          to: '/',
          name: 'name1',
          lable: 'home'
        },
        {
          to: 'other',
          name: 'name2',
          lable: 'Cadastro do salão'
        },
        {
          to: 'other',
          name: 'name3',
          lable: 'Cadastro de parceiros'
        },
        {
          to: 'other',
          name: 'name4',
          lable: 'Visualizar NFSe'
        },
        {
          to: 'other',
          name: 'name5',
          lable: 'Visualizar DAS'
        }
      ]
    }
  },
  methods: {}
}
</script>
