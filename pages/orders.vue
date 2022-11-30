<template>
  <v-card>
    <v-card-title>
      Orders
      <v-spacer></v-spacer>

      <v-text-field v-model="search" append-icon="mdi-magnify" label="Search" single-line hide-details></v-text-field>
    </v-card-title>
    <v-data-table :headers="headers" :items="items" :search="search" :items-per-page="5"></v-data-table>
  </v-card>
</template>
  
<script>
import axios from 'axios'
import moment from 'moment';

export default {

  data() {
    return {
      headers: [{
        text: 'ID',
        value: 'id'
      },

      {
        text: 'Order Date',
        value: 'created_at'
      },
      {
        text: 'Order Name',
        value: 'order_name'
      },
      {
        text: 'Customer ID',
        value: 'customer_id'
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
      axios.get(`http://localhost:8000/orders`)
        .then((response) => {
          this.items = response.data.data.map((item) => {
            return {
              ...item,
              created_at: moment(item.created_at).format('MMMM Do YYYY, h:mm:ss a'),
            }
          })
          
        }).catch((error) => {
          console.log(error)
        })
    },
  }
  
}
</script>