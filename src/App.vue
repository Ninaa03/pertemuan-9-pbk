<script setup>
import ChildComponent from './components/ChildComponent.vue'
import { ref, computed } from 'vue'

const daftarMatkul = [
  { nama: 'PEMROGRAMAN BERBASIS KOMPONEN', dosen: 'M RIZKY FADHILAH, ST,.MKom' },
  { nama: 'ELEKTRONIKA DIGITAL', dosen: 'DRr.EVIZAL, ST.,Meng' },
  { nama: 'PEMROGRAMAN BERORIENTASI OBJEK', dosen: 'AKMAR EFENDI, S.Kom., M.kom' }
]

const selectedIndex = ref(0)
const dipilih = ref('')
const dihapus = ref(false)

const selectedCourse = computed(() => {
  return daftarMatkul[selectedIndex.value] || null
})

function handleAmbil(nama) {
  dipilih.value = nama
  dihapus.value = false
}

function handleHapus(nama) {
  dihapus.value = true
  dipilih.value = ''
}
</script>

<template>
  <div>
    <h1>Sistem KRS - Pilih Mata Kuliah</h1>

    <label>Pilih mata kuliah:</label>
    <select v-model="selectedIndex">
      <option v-for="(matkul, index) in daftarMatkul" :key="index" :value="index">
        {{ matkul.nama }}
      </option>
    </select>

    <ChildComponent
      v-if="selectedCourse && !dihapus"
      :courseName="selectedCourse.nama"
      :lecturer="selectedCourse.dosen"
      @ambil="handleAmbil"
      @hapus="handleHapus"
    >
      <template #note>
        <p>📌 Harap lengkapi prasyarat sebelum mengambil mata kuliah ini.</p>
      </template>
    </ChildComponent>

    <p v-if="dipilih">
      ✔ Anda telah mengambil: <strong>{{ dipilih }}</strong>
    </p>

    <p v-if="dihapus" style="color: red;">
      ❌ Mata kuliah "{{ selectedCourse.nama }}" telah dihapus.
    </p>
  </div>
</template>

<style scoped>
select {
  margin-bottom: 20px;
  padding: 6px 12px;
}
</style>