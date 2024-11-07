<template>
  <div>
    <nav>
      <router-link to="/">Головна</router-link>
      <router-link to="/changed-rates">Змінені курси</router-link>
      <router-link to="/search-rates">Пошук курсу</router-link>
    </nav>
    <router-view />
  </div>
</template>
