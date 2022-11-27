<template>
  <v-card>
    <v-card-title>
      Customer Companies
      <v-spacer></v-spacer>

      <v-text-field v-model="search" append-icon="mdi-magnify" label="Search" single-line hide-details></v-text-field>
    </v-card-title>
    <v-data-table :headers="headers" :items="rows" :search="search"></v-data-table>
  </v-card>
</template>
  
<script>
export default {

  async asyncData(context) {
    let response = await context.$axios.$get('http://localhost:8000/customer_company')
    let dataList = response.data.data.map(item => item)
    return dataList
  },

  data() {

    return {
      
      search: '',
      headers: [{
        text: 'ID',
        value: 'id'
      },

      {
        text: 'Company Name',
        value: 'company_name'
      },
      {
        text: 'Company Id',
        value: 'company_id'
      },

      ],
    }

  },
}
</script>