<template>
  <div>
    <CurrencySearch @search="updateSearch" />
    <ul v-if="filteredCurrencies.length > 0">
      <li v-for="currency in paginatedCurrencies" :key="currency.r030">
        <span>{{ currency.txt }} ({{ currency.cc }}): {{ currency.rate }}</span>
        <router-link :to="`/currency-edit/${currency.r030}`">Редагувати</router-link>
      </li>
    </ul>
    <p v-else>Нічого не знайдено</p>
    <Pagination
      v-if="filteredCurrencies.length > 0"
      :totalItems="filteredCurrencies.length"
      :itemsPerPage="itemsPerPage"
      @pageChanged="changePage"
    />
  </div>
</template>

<script setup>
  import { ref, computed } from "vue";
  import CurrencySearch from "./CurrencySearch.vue";
  import Pagination from "./Pagination.vue";
  import { defineProps } from "vue";

  const props = defineProps({
    currencies: {
      type: Array,
      required: true,
    },
  });

  const currentPage = ref(1);
  const itemsPerPage = 10;
  const searchTerm = ref("");

  const filteredCurrencies = computed(() => {
    if (!searchTerm.value) return props.currencies;
    return props.currencies.filter((currency) =>
      currency.txt.toLowerCase().includes(searchTerm.value.toLowerCase())
    );
  });

  const paginatedCurrencies = computed(() => {
    const start = (currentPage.value - 1) * itemsPerPage;
    return filteredCurrencies.value.slice(start, start + itemsPerPage);
  });

  const changePage = (newPage) => {
    currentPage.value = newPage;
  };

  const updateSearch = (term) => {
    searchTerm.value = term;
    currentPage.value = 1;
  };
</script>
