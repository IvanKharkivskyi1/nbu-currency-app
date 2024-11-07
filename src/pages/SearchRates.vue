<template>
  <div>
    <h1>Пошук курсу за датою</h1>
    <input type="date" v-model="selectedDate" @change="fetchByDate" />
    <CurrencyList :currencies="currencies" />
  </div>
</template>
  
<script setup>
  import { ref } from 'vue';
  import CurrencyList from '../components/CurrencyList.vue';
  import { useCurrencyStore } from '../store/currencyStore';
  
  const store = useCurrencyStore();
  const selectedDate = ref(store.date);
  
  const fetchByDate = () => {
    store.fetchCurrencies(selectedDate.value);
  };
</script>
  