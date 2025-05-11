<template>
    <div class="card">
      <h3>{{ courseName }}</h3>
      <p>Dosen: {{ lecturer }}</p>
  
      <button @click="ambilMatkul">Ambil Mata Kuliah</button>
      <button @click="hapusMatkul" class="hapus">Hapus</button>
  
      <div class="note">
        <slot name="note">Tidak ada catatan tambahan</slot>
      </div>
    </div>
  </template>
  
  <script setup>
  const props = defineProps({
    courseName: String,
    lecturer: String
  })
  
  const emit = defineEmits(['ambil', 'hapus'])
  
  function ambilMatkul() {
    emit('ambil', props.courseName)
  }
  
  function hapusMatkul() {
    emit('hapus', props.courseName)
  }
  </script>
  
  <style scoped>
  .card {
    border: 2px solid #42b883;
    padding: 20px;
    border-radius: 10px;
    width: 300px;
  }
  button {
    margin-top: 10px;
    padding: 6px 12px;
    background-color: #35495e;
    color: white;
    border: none;
    cursor: pointer;
    margin-right: 10px;
  }
  button.hapus {
    background-color: #e74c3c;
  }
  .note {
    margin-top: 12px;
    font-size: 14px;
    color: #555;
    font-style: italic;
  }
  </style>