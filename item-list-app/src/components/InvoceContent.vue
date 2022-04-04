<template>
    <section class="bg-gray-900 w-1/3 mx-auto mt-10 p-2 px-5 rounded-md shadow-2xl">
      <!-- FAtura Bilgileri -->
      
     <InvoceContactInfo :contact="state.contact" />

      <div class="mt-5">
        <heading title="Fatura Kalemleri" />
        <InvoceItems :items="state.items" :AddInvoceItem="AddInvoceItem"/>
        
      </div>
      <!-- Summary -->
      <InvoceSummary :items="state.items"/>

      <hr class="bg-gradient-to-r h-[1px] border-none from-gray-700 mt-5" />
      <div class="actionbar text-right my-5">
        <button @click="onSubmit" class="purple-button">Kaydet</button>
      </div>
    </section>
</template>
<script setup>
import {provide, reactive,watch} from "vue"
import InvoceItems from './InvoceItems.vue';
import InvoceList from './InvoceList.vue';
import InvoceSummary from './InvoceSummary.vue';
import InvoceContactInfo from './InvoceContactInfo.vue';

const props = defineProps({saveInvoce:Function,activeInvoce: [Object, null]})
const state = reactive({
  contact:{
    contact_name:null,
    email:null,
    city:null,
    country:null,
    zipcode:null,
    country:null,
    
  },
  items:[],
})
const AddInvoceItem = () =>{
  state.items.push({
    id:new Date().getTime(),
    name:null,
    qty:null,
    unit_price:null,
    total_price:0.0,
  })
}
const DeleteInvoceItem = (invoceItem) =>{
  //state.items = state.items.filter(i => i.id !== invoceItem.id)
  //console.log((state.items).indexOf(invoceItem.id))
  //state.items = state.items.splice(state.items.findIndex(invoceItem.id === state.items.id),1)
  let index = state.items.indexOf(invoceItem)
  console.log(index)
  state.items.splice(index,1)

}
provide("DeleteInvoceItem",DeleteInvoceItem)
const onSubmit = () =>{
   console.log(state)
   props.saveInvoce({...state,created_at:new Date(),id:new Date().getTime()})
   state.contact ={
     
    contact_name:null,
    email:null,
    city:null,
    country:null,
    zipcode:null,
    country:null,
    
  
   }
   state.items = [];
}
provide("AddInvoceItem",AddInvoceItem)
watch(
  () => props.activeInvoce,
  (activeInvoce) => {
    if (activeInvoce) {
      state.contact = {
        ...activeInvoce.contact,
      };
      state.items = [...activeInvoce.items];
    }
  }
);
</script>
