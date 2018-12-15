<template>
    <div>
        <h1>Product List</h1>   
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
          variant: "danger"
        }
      ]
    };
  },
  mounted() {
    var instance = this;
    axios
      .get("https://vast-oasis-47337.herokuapp.com/api/supplier")
      .then(function(response) {
        console.log(response.data);
        instance.products = response.data.data;
      });
  }
};
</script>