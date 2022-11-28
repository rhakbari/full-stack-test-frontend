<template>
  <v-card>
    <v-card-title>
      Customers
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
        text: 'User ID',
        value: 'user_id'
      },
      {
        text: 'Name',
        value: 'name'
      },
      {
        text: 'Company ID',
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
    showEditDialog(item) {
      this.editedItem = item || {}
      this.dialog = !this.dialog
    },
    loadItems() {
      this.items = []
      axios.get(`http://localhost:8000/customers`)
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