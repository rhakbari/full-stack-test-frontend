<template>
  <v-card>
    <v-card-title>
      Customer Companies
      <v-spacer></v-spacer>

      <v-text-field v-model="search" append-icon="mdi-magnify" label="Search" single-line hide-details></v-text-field>
    </v-card-title>
    <v-data-table :headers="headers" :items="items" :search="search"></v-data-table>
  </v-card>
</template>
  
<script>
import axios from 'axios'
export default {

 data() {
    return {
      headers: [{
        text: 'ID',
        value: 'id'
      },

      {
        text: 'Order ID',
        value: 'order_id'
      },
      {
        text: 'Price Per Unit',
        value: 'price_per_unit'
      },
      {
        text: 'Quantity',
        value: 'quantity'
        },
        {
        text: 'Product',
        value: 'product'
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
    showEditDialog(item) {
      this.editedItem = item || {}
      this.dialog = !this.dialog
    },
    loadItems() {
      this.items = []
      axios.get(`http://localhost:8000/order_items`)
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