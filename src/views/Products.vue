 <template>
 <b-row>
   
      <b-col md="6" class="my-1">
        <b-form-group horizontal label="Filter" class="mb-0">
          <b-input-group>
            <b-form-input v-model="filter" placeholder="Type to Search" />
            <b-input-group-append>
              <b-btn :disabled="!filter" @click="filter = ''">Clear</b-btn>
            </b-input-group-append>
          </b-input-group>
        </b-form-group>
      </b-col>


  <b-table striped hover :items="items" :fields="fields" :filter="filter" :per-page="pageSize" :current-page="pageIndex">
    <template slot="show_details" slot-scope="row">
      <!-- we use @click.stop here to prevent emitting of a 'row-clicked' event  -->
      <b-button size="sm" @click.stop="row.toggleDetails" class="mr-2">
       {{ row.detailsShowing ? 'Hide' : 'Show'}} Details
      </b-button>
      <!-- In some circumstances you may need to use @click.native.stop instead -->
      <!-- As row.showDetails is one-way, we call the toggleDetails function on @change -->
     
    </template>
    <template slot="row-details" slot-scope="row">
      <b-card>
        <b-row class="mb-2">
          <b-col sm="3" class="text-sm-right"><b>category_id:</b></b-col>
          <b-col>{{ row.item.category_id }}</b-col>
        </b-row>
        <b-row class="mb-2">
          <b-col sm="3" class="text-sm-right"><b>category_name:</b></b-col>
          <b-col>{{ row.item.category_name }}</b-col>
        </b-row>
        <b-row class="mb-2">
          <b-col sm="3" class="text-sm-right"><b>description:</b></b-col>
          <b-col>{{ row.item.description }}</b-col>
        </b-row>
        <b-row class="mb-2">
          <b-col sm="3" class="text-sm-right"><b>picture:</b></b-col>
          <b-col>{{ row.item.picture }}</b-col>
        </b-row>
        <b-button size="sm" @click="row.toggleDetails">Hide Details</b-button>
      </b-card>
    </template>
  </b-table>
   <b-col md="6" class="my-1">
  <b-pagination align="center" size="md" :total-rows="items.length" v-model="pageIndex" :per-page="pageSize">
    </b-pagination> 
     </b-col>
    <br>
 <b-col md="6" class="my-1">
    <div>CurrentPage: {{pageIndex}}</div>  
     </b-col>
  </b-row>
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