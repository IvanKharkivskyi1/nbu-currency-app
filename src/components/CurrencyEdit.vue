<template>
  <div>
    <h1>Редагування валюти</h1>
    <div v-if="currency">
      <h2>{{ currency.txt }} ({{ currency.cc }})</h2>
      <label for="rate">Курс:</label>
      <input type="number" v-model="currency.rate" />
      <button @click="saveCurrency">Зберегти</button>
      <router-link to="/changed-rates">Назад до змінених курсів</router-link>
    </div>
    <div v-else>
      <p>Завантаження...</p>
    </div>
  </div>
</template>

<script setup>
  import { ref, onMounted } from "vue";
  import { useRoute, useRouter } from "vue-router";
  import { useCurrencyStore } from "../store/currencyStore";

  const route = useRoute();
  const router = useRouter();
  const store = useCurrencyStore();
  const currency = ref(null);

  onMounted(() => {
    const currencyId = parseInt(route.params.id);
    const foundCurrency = store.currencies.find((c) => c.r030 === currencyId);
    if (foundCurrency) {
      currency.value = { ...foundCurrency };
    }
  });

  const saveCurrency = () => {
    if (currency.value) {
      store.addEditedCurrency(currency.value);
      router.push("/changed-rates");
    }
  };
</script>
