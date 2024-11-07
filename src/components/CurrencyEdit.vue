<template>
    <div>
        <h1>Редагувати курс для {{ currency?.txt }}</h1>
        <label>
        Новий курс:
        <input type="number" v-model.number="newRate" />
        </label>
        <button @click="saveCurrency">Зберегти</button>
        <button @click="cancelEdit">Скасувати</button>
    </div>
</template>
  
<script setup>
  import { ref, onMounted } from 'vue';
  import { useRouter, useRoute } from 'vue-router';
  import { useCurrencyStore } from '../store/currencyStore';
  
  const store = useCurrencyStore();
  const router = useRouter();
  const route = useRoute();
  
  const currencyId = route.params.id;
  const currency = ref(null);
  const newRate = ref(0);

  onMounted(() => {
    currency.value = store.currencies.find(item => item.r030 === Number(currencyId));
    if (currency.value) {
      newRate.value = currency.value.rate;
    }
  });
  
  const saveCurrency = () => {
    if (currency.value) {
      const updatedCurrency = { ...currency.value, rate: newRate.value };
      store.addEditedCurrency(updatedCurrency);
      router.push('/changed-rates');
    }
  };
  
  const cancelEdit = () => {
    router.push('/');
  };
</script>
  