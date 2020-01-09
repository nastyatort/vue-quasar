<template>
<div class="main-wrapper">
  <div class="container">
    <div class="main">
      <div class="filter-wrapper row justify-between items-center">
        <div class="filter-item date-item">
          <div class="title">periodo</div>
          <div class="date-wrapper row justify-between items-center">
            <q-input v-model="dateFrom" mask="date" :rules="['date']">
              <template v-slot:append>
                <div name="event" class="cursor-pointer date-icon">
                  <q-popup-proxy ref="qDateProxy" transition-show="scale" transition-hide="scale">
                    <q-date @click="selectCategory = 'dateFrom'" minimal today-btn v-model="dateFrom" @input="() => $refs.qDateProxy.hide()" />
                  </q-popup-proxy>
                </div>
              </template>
            </q-input>

            <q-input v-model="dateTo" mask="date" :rules="['date']">
              <template v-slot:append>
                <div name="event" class="cursor-pointer date-icon">
                  <q-popup-proxy ref="qDateProxyTo" transition-show="scale" transition-hide="scale">
                    <q-date @click="selectCategory = 'dateTo'" minimal today-btn v-model="dateTo" @input="() => $refs.qDateProxyTo.hide()" />
                  </q-popup-proxy>
                </div>
              </template>
            </q-input>
          </div>
        </div>
        <div class="filter-item">
          <div class="title">tipo de serviço</div>
          <q-input placeholder="tipo de serviço" v-model="type" type="text" @keyup="selectCategory = 'type'">
            <template>
              <q-avatar>
                <img src="../statics/icons/search.png" />
              </q-avatar>
            </template>
          </q-input>
        </div>
        <div class="filter-item" @click="selectCategory = 'name'">
          <div class="title">Parceiro selecionado</div>
          <q-select label="Parceiro selecionado" v-model="name" type="text" :options="selectOptions()" />
        </div>
      </div>
      <Table :filter='filter' :formatDate='formatDate' :showId='showId'></Table>
      <div class="button-wrapper row items-center">
        <q-btn @click="clearFilter" rounded id="report" label="Clear filter" />
        <q-btn @click="report" rounded id="gerar" label="gerar relatório" />
      </div>
    </div>
  </div>
</div>
</template>

<script>
import moment from 'moment'
import Table from './Table.vue'

export default {
  name: 'Filters',
  components: {
    Table
  },
  data () {
    return {
      type: '',
      name: '',
      selectCategory: 'all',
      table: 'table.png',
      dateFrom: this.formatDate(new Date('2019-01-01')),
      dateTo: this.formatDate(new Date('2019-04-01')),
      date: this.formatDate(new Date('2019-02-07')),
      title: [{
        name: 'name',
        required: true,
        label: 'Parceiro',
        align: 'left',
        field: row => row.name,
        format: val => `${val}`,
        sortable: true
      },
      {
        name: 'cnpj',
        field: 'cnpj',
        required: true,
        label: 'CNPJ',
        align: 'left',
        sortable: true
      },
      {
        name: 'dateFrom',
        field: 'dateFrom',
        required: true,
        label: 'Período De',
        align: 'left',
        sortable: true
      },
      {
        name: 'dateTo',
        field: 'dateTo',
        required: true,
        label: 'Período Até',
        align: 'left',
        sortable: true
      },
      {
        name: 'coast',
        field: 'coast',
        required: true,
        label: 'Valor R',
        align: 'left',
        sortable: true
      },
      {
        name: 'type',
        field: 'type',
        required: true,
        label: 'Tipo De Serviço',
        align: 'left',
        sortable: true
      },
      {
        name: 'Açao',
        field: 'acao',
        required: true,
        label: 'Açao',
        align: 'left',
        sortable: true
      }
      ],
      info: [{
        id: '1id',
        name: 'Jozé da Silva Sauro',
        cnpj: '00.89.89/0001-09',
        dateFrom: new Date('2040-01-01'),
        dateTo: new Date('2051-01-01'),
        coast: '100,00',
        type: 'Cabeleireiro aa'
      },
      {
        id: '2id',
        name: 'Neideleine Rocha Nide',
        cnpj: '00.89.89/0001-09',
        dateFrom: new Date('2030-01-01'),
        dateTo: new Date('2031-01-01'),
        coast: '189,00',
        type: 'Barbeiro'
      },
      {
        id: '3id',
        name: 'Jozé da Silva Sauro',
        cnpj: '00.89.89/0001-09',
        dateFrom: new Date('2023-01-01'),
        dateTo: new Date('2024-01-01'),
        coast: '100,00',
        type: 'Cabeleireiro aa'
      },
      {
        id: '4id',
        name: 'aa',
        cnpj: '00.89.89/0001-09',
        dateFrom: new Date('2021-01-01'),
        dateTo: new Date('2022-01-01'),
        coast: '100,00',
        type: 'aa'
      },
      {
        id: '5id',
        name: 'bb',
        cnpj: '00.89.89/0001-09',
        dateFrom: new Date('2020-01-01'),
        dateTo: new Date('2021-01-01'),
        coast: '100,00',
        type: 'bb'
      }
      ]
    }
  },
  methods: {
    selectOptions () {
      const selectList = this.info.map(item => item.name)
      return ['all', ...new Set(selectList)]
    },
    clearFilter () {
      this.type = ''
      this.name = ''
      this.dateFrom = this.formatDate(new Date('2019-01-01'))
      this.dateTo = this.formatDate(new Date('2019-04-01'))
    },
    report () {
      console.log('show report')
    },
    showId (id) {
      alert(id)
    },
    formatDate: function (dt) {
      return moment(String(dt)).format('YYYY/MM/DD')
    }
  },
  computed: {
    filter () {
      let filteredInfo = this.info
      console.log(filteredInfo)
      switch (this.selectCategory) {
        case 'all':
          return this.info
        case 'name':
          if (this.name !== '' && this.name !== 'all') {
            return this.info.filter(el => el.name === this.name)
          } else {
            return this.info
          }
        case 'type':
          return this.info.filter(
            el => el.type.toLowerCase().indexOf(this.type.toLowerCase()) !== -1
          )
        case 'dateFrom':
          return this.info.filter(el => this.formatDate(el.dateFrom) > this.dateFrom)
        case 'dateTo':
          return this.info.filter(el => this.formatDate(el.dateTo) < this.dateTo)
        default:
          return this.info
      }
    }
  }
}
</script>
