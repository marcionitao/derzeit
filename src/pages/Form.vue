<template>
<q-page padding>
  <h4>Adicionar Produtos</h4>

  <pre>{{product}}</pre>

  <q-form class="row q-col-gutter-md" @submit.prevent="addForm" @reset="addClear" ref="myForm">
    <div class="col-12 col-sm-6">
      <q-input
        v-model="product"
        label="Product"
        lazy-rules
        :rules="[val => val && val.length > 0 || 'Please type something']"
      />
    </div>
     <div class="col-12 col-sm-6">
       <q-select
          v-model="selected"
          :options="myoptions"
          label="Prioridad"
          lazy-rules
          :rules="[val => val && val.length > 0 || 'Please type something']"
        />
    </div>
    <div class="col-12">
      <q-toggle v-model="conditions" color="green" label="Conditions accepted"/>
    </div>
    <!--Buttons-->
    <div class="col-12 q-gutter-sm">
      <q-btn color="secondary" label="Submit" type="submit"/>
      <q-btn color="secondary" outline label="Reset" type="reset"/>
    </div>
  </q-form>

  <!--Son Component(ShowDatas)-->
  <show-datas :products='products' />
</q-page>
</template>

<script>
import { ref } from 'vue'
import { useQuasar } from 'quasar'
import ShowDatas from '../components/ShowDatas'

export default {
  
  components: { ShowDatas },

  setup() {
    // used quasar pluggin
    const $q = useQuasar();

    const myForm = ref(null);
    const product = ref(null);
    const selected = ref(null);
    const conditions = ref(false);
    const myoptions = ['maxima', 'moderada', 'minima'];

    // use for show ours data table as 'Props'
    const products = ref([]);

    const addForm = () => {
      if (conditions.value === false) {
        $q.notify({
          color: 'red-5',
          textColor: 'white',
          position: 'top',
          icon: 'warning',
          message:'You have to accept the conditions!'}
        )
      }else{
        $q.notify({
          color: 'green-4',
          textColor: 'white',
          position: 'top',
          icon: 'cloud-done',
          message:'Submited!'}
        )
        // reset Form
        myForm.value.resetValidation();

        // processing Form
        products.value = [...products.value, {
          product: product.value,
          prioridad: selected.value
        }]
        console.log([...products.value])

        // clear Form
        addClear();

      }

    }
    // clear Form
    const addClear = () => {
      product.value = null;
      selected.value = null;
      conditions.value = false;
    }

    return {
      myForm, product, selected, myoptions, addForm, conditions, addClear, products
    }
  }
}
</script>
