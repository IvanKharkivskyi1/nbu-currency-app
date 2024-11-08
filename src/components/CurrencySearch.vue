<template>
    <div class="search-date-container">
      <input
        type="search"
        v-model="searchTerm"
        placeholder="Шукати валюту..."
        @input="filterCurrencies"
      />
    </div>
</template>
  
<script setup>
  import { ref, defineEmits } from 'vue';
  
  const emit = defineEmits(['search']);
  
  const searchTerm = ref('');

  const filterCurrencies = () => {
    emit('search', searchTerm.value);
  };
</script>
  