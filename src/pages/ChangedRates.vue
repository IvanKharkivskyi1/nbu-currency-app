<template>
  <div>
    <h1>Змінені курси валют</h1>
    <CurrencyList :currencies="editedCurrencies" />
  </div>
</template>

<script setup>
  import { computed } from 'vue';
  import CurrencyList from '../components/CurrencyList.vue';
  import { useCurrencyStore } from '../store/currencyStore';

  const store = useCurrencyStore();
  const editedCurrencies = computed(() => store.editedCurrencies);
</script>
