<template>
    <div class="hotel-detail">
      <h2>{{ hotel.name }}</h2>
      <p>{{ hotel.description }}</p>
      <h3>Fasilitas:</h3>
      <ul>
        <li v-for="(amenity, index) in hotel.amenities" :key="index">{{ amenity }}</li>
      </ul>
    </div>
  </template>
  
  <script setup>
  import { defineProps } from 'vue';
  
  const props = defineProps({
    hotel: Object
  });
  </script>
  
  <style scoped>
  .hotel-detail {
    border: 1px solid #ccc;
    padding: 16px;
    border-radius: 8px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  }
  h3 {
    margin-right: -100px;
  }
  </style>
  