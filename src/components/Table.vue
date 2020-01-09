<template>
      <div class="table-wrapper">
        <div class="table__title">
          <div class="table__icon">
            <img src="../statics/icons/table.png" />
          </div>
          <h2>NFSe</h2>
        </div>
        <q-table table-header-class="table-header" table-class="table" :data="filter" :columns="title" hide-bottom row-key="id">
          <template v-slot:body="props">
            <q-tr :props="props">
              <q-td key="name" :props="props">{{ props.row.name }}</q-td>
              <q-td key="cnpj" :props="props">{{ props.row.cnpj }}</q-td>
              <q-td key="dateFrom" :props="props">{{ formatDate(props.row.dateFrom) }}</q-td>
              <q-td key="dateTo" :props="props">{{ formatDate(props.row.dateTo) }}</q-td>
              <q-td key="coast" :props="props">{{ props.row.coast }}</q-td>
              <q-td key="type" :props="props">{{ props.row.type }}</q-td>
              <q-td key="acao">
                <span class="show" @click="showId(props.row.id)"></span>
              </q-td>
            </q-tr>
          </template>
        </q-table>
      </div>
</template>

<script>
export default {
  name: 'Table',
  props: ['filter', 'formatDate', 'showId'],
  data () {
    return {
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
  }
}
</script>
