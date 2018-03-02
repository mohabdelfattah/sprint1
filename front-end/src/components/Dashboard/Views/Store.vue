<template>
  <div>
     <input type="text" v-model= "name" > Name <br>
     <input type="text" v-model= "price" > Price <br>
     <input type="text" v-model= "deleteP" > product delete <br>
    
     <button v-on:click="createbooky"> add </button>
     <button v-on:click="deletebooky"> delete </button>


   <!-- <label> Item name:</label>
  <input type= "text" v-model= "cname">
  <label> Item price:</label>
  <input type= "text" v-model= "cprice"> -->

  <table style="width:100%">
  <tr>
    <th>ID</th>
    <th>Name</th>
    <th>Price</th>
    <th>Created at</th>
    <th>Updated at</th>
    <th>Seller Name</th>
  </tr>
      <tbody>
        <tr v-for="row in items.data">
          <td>{{ row._id }}</td>
          <td>{{ row.name }}</td>
          <td>{{ row.price }}</td>
          <td>{{ row.createdAt }}</td>
          <td>{{ row.UpdatedAt }}</td>
          <td>{{ row.sellerName }}</td>

        </tr>

      </tbody>
</table>
</div>
</template>
<script>
import PaperTable from 'components/UIComponents/PaperTable.vue'
import axios from 'axios'
export default {
  components: {
    PaperTable
  },
  data () {
    return {
      table: {
        title: 'Products',
        subTitle: '',
        columns: ['ID', 'Name', 'Salary', 'Country', 'City', 'Edit'],
        data: [{
          id: 1,
          name: 'Dakota Rice',
          salary: '$36.738',
          country: 'Niger',
          city: 'Oud-Turnhout'
        },
        {
          id: 2,
          name: 'Minerva Hooper',
          salary: '$23,789',
          country: 'Curaçao',
          city: 'Sinaai-Waas'
        },
        {
          id: 3,
          name: 'Sage Rodriguez',
          salary: '$56,142',
          country: 'Netherlands',
          city: 'Baileux'
        },
        {
          id: 4,
          name: 'Philip Chaney',
          salary: '$38,735',
          country: 'Korea, South',
          city: 'Overland Park'
        },
        {
          id: 5,
          name: 'Doris Greene',
          salary: '$63,542',
          country: 'Malawi',
          city: 'Feldkirchen in Kärnten'
        }]

      },
      items: [],
      name: '',
      price: ''
    }
  },
  created () {
    this.getbooky()
  },
  methods: {
    getbooky () {
      axios.get('http://localhost:3000/api/product/getProducts')
    .then((response) => {
      this.items = response.data
      console.log(response)
    })
    .catch((error) => {
      console.log(error)
    })
    },
    createbooky () {
      axios.post('http://localhost:3000/api/product/createProduct', {
        name: this.name,
        price: this.price
      }).then((response) => {
        console.log(response)
      })
  .catch((error) => {
    console.log(error)
  })
    },
    deletebooky () {
      axios.delete('http://localhost:3000/api/product/deleteProduct' + this.id)
      .then((response) => {
        console.log(response)
      })
      .catch((error) => {
        console.log(error)
      })
    }
  }
}

</script>
