<template>
    <div>
        <h1>Suppliers</h1>   
         <b-table striped hover :items="products" :fields="fields" :per-page="pageSize" :current-page="pageIndex" ></b-table>
           <b-pagination size="md" :total-rows="products.length" v-model="pageIndex" :per-page="pageSize"></b-pagination>
    </div>
</template>
<script>
import axios from "axios";

export default {
  name: "Suppliers",
  data() {
    return {
      message: "Project 2",
      pageSize: 10,
      pageIndex: 1,
      products: [],
      fields: [
        {
          key: "supplier_id",
          sortable: true
        },
        {
          key: "company_name",
          sortable: true
        },
        {
          key: "contact_name",
          sortable: true
        },
        {
          key: "address",
          sortable: true
        },
        {
          key: "city",
          sortable: true
        },
        {
          key: "region",
          sortable: true
        },
        {
          key: "postal_code",
          sortable: true
        },
        {
          key: "country",
          sortable: true
        },
        {
          key: "phone",
          sortable: true
        },
        {
          key: "fax",
          sortable: true
        },
        {
          key: "homepage",
          sortable: true,
        },
        {
          key: "key:  'show_details'",
        }
      ]
    };
  },
   computed: {
    sortOptions () {
      // Create an options list from our fields
      return this.fields
        .filter(f => f.sortable)
        .map(f => { return { text: f.label, value: f.key } })
    }
  },
  async mounted() {
    let products = await axios.get(
      "https://vast-oasis-47337.herokuapp.com/api/supplier"
    );
    products = products.data.data;
    this.items = products;
   
  }
}
</script>