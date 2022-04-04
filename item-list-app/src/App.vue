
  <template>
  <div class="w-screen h-screen bg-gray-800 flex flex-row text-white items-start justify-center">
    <AppSideBar :invoces="invoceList" :editInvoce="editInvoce"  />
    <InvoceContent :saveInvoce="saveInvoce" :activeInvoce="state.activeInvoce"/>
    
    
    
    
  </div>
</template>
<script setup>
import { reactive, ref } from 'vue';
import AppSideBar from './components/AppSideBar.vue';
import InvoceContent from "./components/InvoceContent.vue";
const state = reactive({activeInvoce:null})
const invoceList = ref([
  {
    id: new Date().getTime(),
    contact: {
      contact_name: "Demo 1",
      email: "demo@demo.com",
      city: "Marmaris",
      country: "Demo Country",
      zipcode: "DemoZipCode",
    },
    items: [
      {
        id: new Date().getTime(),
        name: "Demo Ürün",
        qty: 1,
        unit_price: 10.0,
        total_price: 10.0,
      },
    ],
  },
]);
const saveInvoce = (invoce) =>{
  invoceList.value.push(invoce)

}
const editInvoce = (invoce) =>{
  console.log(invoce)
  state.activeInvoce = invoce;

}

</script>
