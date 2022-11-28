<template>
  <v-card>
    <v-card-title>
      Customer Companies
      <v-spacer></v-spacer>

      <v-text-field v-model="search" append-icon="mdi-magnify" label="Search" single-line hide-details></v-text-field>
    </v-card-title>
    <v-data-table :headers="headers" :items="items" :search="search" :items-per-page="5"></v-data-table>
  </v-card>
</template>
  
<script>
import axios from 'axios'
export default {

  data() {
    return {
      headers: [{
        text: 'ID',
        value: 'ID'
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
      items: [],
      search: '',
    }

  },

  mounted() {
    this.loadItems()
  },

  methods: {
   
    loadItems() {
      this.items = []
      axios.get(`http://localhost:8000/customer_company`)
        .then((response) => {
          this.items = response.data.data.map((item) => {
            return {
            
              ...item
            }
          })
        }).catch((error) => {
          console.log(error)
        })
    },

  }
}
</script>