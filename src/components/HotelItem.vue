<template>
    <div class="hotel-card">
      <img :src="hotel.imageUrl" alt="Foto Hotel" class="hotel-image" />
      <div class="hotel-info">
        <h2>{{ hotel.name }}</h2>
        <button class="detail-button" @click="showDetail">Lihat Detail</button>
      </div>
    </div>
  </template>
  
  <script setup>
  import { defineProps } from 'vue';
  
  const props = defineProps({
    hotel: Object
  });
  
  const emit = defineEmits(['show-detail']);
  
  function showDetail() {
    emit('show-detail', props.hotel);
  }
  </script>
  
  <style scoped>
  .hotel-card {
    border: 1px solid #ccc;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s;
  }
  
  .hotel-card:hover {
    transform: scale(1.05);
  }
  
  .hotel-image {
    width: 100%;
    height: 200px;
    object-fit: cover;
    border-radius: 8px 8px 0 0;
  }
  
  .hotel-info {
    padding: 16px;
  }
  
  .hotel-info h2 {
    margin: 0 0 8px;
    font-size: 1.2em;
  }
  
  .detail-button {
    background-color: #007bff;
    color: #fff;
    border: none;
    padding: 8px 16px;
    border-radius: 4px;
    cursor: pointer;
    width: 100%;
    max-width: 200px;
  }
  
  .detail-button:hover {
    background-color: #0056b3;
  }
  </style>
  