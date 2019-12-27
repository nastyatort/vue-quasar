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
            <q-date v-on:click="selectCategory = 'dateFrom'" minimal today-btn v-model="dateFrom" @input="() => $refs.qDateProxy.hide()" />
          </q-popup-proxy>
        </div>
      </template>
    </q-input>

          <q-input v-model="dateTo" mask="date" :rules="['date']">
      <template v-slot:append>
        <div name="event" class="cursor-pointer date-icon">
          <q-popup-proxy ref="qDateProxyTo" transition-show="scale" transition-hide="scale">
            <q-date v-on:click="selectCategory = 'dateTo'" minimal today-btn v-model="dateTo" @input="() => $refs.qDateProxyTo.hide()" />
          </q-popup-proxy>
        </div>
      </template>
    </q-input>
             </div>
        </div>
          <div class="filter-item">
            <div class="title">tipo de serviço</div>
            <q-input placeholder="tipo de serviço" v-model="type" type="text">
              <template>
                <q-avatar v-on:click="selectCategory = 'type'">
                  <img src="../statics/icons/search.png" />
                </q-avatar>
              </template>
            </q-input>
          </div>
          <div class="filter-item" v-on:click="selectCategory = 'name'" >
                <div class="title">Parceiro selecionado</div>
                <q-select label="Parceiro selecionado" v-model="name" type="text" :options="selectOptions()"/>
          </div>
        </div>
        <div class="table-wrapper">
             <div class="table__title">
        <div class="table__icon">
            <img src="../statics/icons/table.png" />
        </div>
        <h2>NFSe</h2>
    </div>
    <q-table
      table-header-class="table-header"
      table-class="table"
      :data="filter()"
      :columns="title"
      hide-bottom
      row-key="id"
    >
 <template v-slot:body="props">
        <q-tr :props="props">
          <q-td key="name" :props="props">{{ props.row.name }}</q-td>
          <q-td key="cnpj" :props="props">{{ props.row.cnpj }}</q-td>
          <q-td key="dateFrom" :props="props">{{ props.row.dateFrom }}</q-td>
          <q-td key="dateTo" :props="props">{{ props.row.dateTo }}</q-td>
          <q-td key="coast" :props="props">{{ props.row.coast }}</q-td>
          <q-td key="type" :props="props">{{ props.row.type }}</q-td>
          <q-td key="acao">
            <span class="show" v-on:click="action(props.row.id)"></span>
          </q-td>
        </q-tr>
      </template>
    </q-table>
        </div>
        <div class="button-wrapper row items-center">
            <q-btn v-on:click="clearFilter()" rounded id="report" label="Clear filter" />
            <q-btn v-on:click="report()" rounded id="gerar" label="gerar relatório" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Table',
  data () {
    return {
      type: '',
      name: '',
      selectCategory: 'all',
      table: 'table.png',
      dateFrom: '2019/01/01',
      dateTo: '2019/04/01',
      date: '2019/02/07',
      title: [
        {
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
          label: 'Valor R$',
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
      info: [
        {
          id: '1id',
          name: 'Jozé da Silva Sauro',
          cnpj: '00.89.89/0001-09',
          dateFrom: '2019/02/01',
          dateTo: '2019/02/20',
          coast: '100,00',
          type: 'Cabeleireiro aa'
        },
        {
          id: '2id',
          name: 'Neideleine Rocha Nide',
          cnpj: '00.89.89/0001-09',
          dateFrom: '2019/02/25',
          dateTo: '2019/02/28',
          coast: '189,00',
          type: 'Barbeiro'
        },
        {
          id: '3id',
          name: 'Jozé da Silva Sauro',
          cnpj: '00.89.89/0001-09',
          dateFrom: '2019/02/01',
          dateTo: '2019/02/10',
          coast: '100,00',
          type: 'Cabeleireiro aa'
        }
      ]
    }
  },
  methods: {
    filter () {
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
          return this.info.filter(el => el.dateFrom > this.dateFrom)
        case 'dateTo':
          return this.info.filter(el => el.dateTo < this.dateTo)
      }
    },
    selectOptions () {
      const selectList = this.info.map(item => item.name)
      return ['all', ...new Set(selectList)]
    },
    clearFilter () {
      this.type = ''
      this.name = ''
      this.dateFrom = '2019/01/01'
      this.dateTo = '2019/04/01'
    },
    report () {
      console.log('show report')
    },
    action (id) {
      alert(id)
    }
  }
}
</script>
