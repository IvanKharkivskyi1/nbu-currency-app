<template>
    <div>
      <ul v-if="paginatedCurrencies.length">
        <li v-for="currency in paginatedCurrencies" :key="currency.r030">
          <span @click="editCurrency(currency)" style="cursor: pointer;">
            {{ currency.txt }} ({{ currency.cc }}): {{ currency.rate }}
          </span>
        </li>
      </ul>
      <p v-else>Немає доступних даних для відображення.</p>
      <Pagination :totalItems="currencies.length" :itemsPerPage="10" @pageChanged="changePage" />
    </div>
</template>
  
<script setup>
  import { computed, ref } from 'vue';
  import { useRouter } from 'vue-router';
  import { useCurrencyStore } from '../store/currencyStore';
  import Pagination from './Pagination.vue';
  
  const store = useCurrencyStore();
  const router = useRouter();
  const currentPage = ref(1);
  const currencies = computed(() => store.editedCurrencies.length ? store.editedCurrencies : store.currencies);

  const paginatedCurrencies = computed(() => {
    const start = (currentPage.value - 1) * 10;
    return currencies.value.slice(start, start + 10);
  });

  const changePage = (page) => {
    currentPage.value = page;
  };

  const editCurrency = (currency) => {
    router.push(`/currency-edit/${currency.r030}`);
  };
</script>
  