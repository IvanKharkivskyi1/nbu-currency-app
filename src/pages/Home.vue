<template>
  <div>
    <h1>Курси валют НБУ на сьогодні</h1>
    <CurrencyList :currencies="store.currencies" />
  </div>
</template>

<script setup>
  import { onMounted } from 'vue';
  import CurrencyList from '../components/CurrencyList.vue';
  import { useCurrencyStore } from '../store/currencyStore';

  const store = useCurrencyStore();

  onMounted(() => {
    store.fetchCurrencies();
  });
</script>
