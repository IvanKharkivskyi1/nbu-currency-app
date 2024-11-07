<template>
    <div>
      <button @click="prevPage" :disabled="currentPage === 1">Попередня</button>
      <span>Сторінка {{ currentPage }} з {{ totalPages }}</span>
      <button @click="nextPage" :disabled="currentPage === totalPages">Наступна</button>
    </div>
</template>
  
<script setup>
  import { ref, computed } from 'vue';
  
  const props = defineProps({
    totalItems: Number,
    itemsPerPage: Number,
  });
  const emit = defineEmits(['pageChanged']);
  
  const currentPage = ref(1);
  const totalPages = computed(() => Math.ceil(props.totalItems / props.itemsPerPage));
  
  const prevPage = () => {
    if (currentPage.value > 1) {
      currentPage.value--;
      emit('pageChanged', currentPage.value);
    }
  };
  
  const nextPage = () => {
    if (currentPage.value < totalPages.value) {
      currentPage.value++;
      emit('pageChanged', currentPage.value);
    }
  };
</script>
  