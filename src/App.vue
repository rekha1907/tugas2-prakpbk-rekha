<template>
  <div class="container">
    <div class="header">
    </div>

    <!-- Bagian untuk ayat Al-Qur'an -->
    <div class="quran-container">
      <h2>Kata-Kata Mutiara</h2>
      <!-- Input teks untuk menambahkan ayat Al-Qur'an -->
      <div class="input-container">
        <input type="text" v-model="newVerse" placeholder="Tambahkan Quote versi terbaik anda" class="input-verse">
        <!-- Tombol untuk menambahkan ayat Al-Qur'an -->
        <button @click="addVerse" class="btn-add">Tambahkan</button>
      </div>

      <!-- Daftar ayat Al-Qur'an -->
      <ul class="quran-list">
        <li v-for="(verse, index) in quranVerses" :key="index" class="quran-item">
          {{ verse }}
          <!-- Tombol untuk menghapus ayat Al-Qur'an -->
          <button @click="removeVerse(index)" class="btn-remove">Hapus</button>
        </li>
      </ul>

      <!-- Contoh elemen dengan class dan style bindings yang dikontrol oleh tombol -->
      <div :class="{ 'highlighted': isHighlighted }" :style="{ 'font-size': fontSize + 'px' }" class="example-element">
        ِبِسْمِ اللَّهِ الرَّحْمَنِ الرَّحِيْم
      </div>


      <!-- Tombol untuk mengontrol class dan style bindings -->
      <!-- Tombol untuk mengontrol class dan style bindings -->
    <div class="button-group">
      <button @click="toggleHighlight" class="btn-toggle">Toggle Highlight</button> &nbsp
      <button @click="toggleTextColor" class="btn-toggle">Toggle Text Color</button> &nbsp
      <button @click="toggleFontSize" class="btn-toggle">Toggle Font Size</button> &nbsp
    </div>

    </div>
    <br>

   <!-- Bagian untuk input data Haji dan Umrah -->
<div class="haji-umroh-container">
  <h2>Travel Haji Umroh</h2>
  <form @submit.prevent="submitHajiUmroh">
    <div class="form-group">
      <label for="nama">Nama:</label>
      <input type="text" id="nama" v-model="hajiUmroh.nama" required>
    </div>
    <div class="form-group">
      <label for="hajiUmroh">Haji/Umroh:</label>
      <select id="hajiUmroh" v-model="hajiUmroh.hajiUmroh" required class="form-select">
        <option v-for="option in hajiUmrohOptions" :key="option" :value="option">{{ option }}</option>
      </select>
    </div>
    <div class="form-group">
      <label for="tahun">Tahun Keberangkatan:</label>
      <input type="number" id="tahun" v-model="hajiUmroh.tahun" required class="form-input">
    </div>
    <div class="form-group">
      <label for="tabungan">Tabungan:</label>
      <input type="number" id="tabungan" v-model="hajiUmroh.tabungan" required class="form-input">
    </div>
    <button type="submit" class="btn-submit">Submit</button>
  </form>

  <!-- Tabel untuk menampilkan data Haji dan Umrah -->
  <table v-if="hajiUmrahData.length > 0" class="haji-umrah-table">
    <thead>
      <tr>
        <th>Nama</th>
        <th>Haji/Umroh</th>
        <th>Tahun Keberangkatan</th>
        <th>Tabungan</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(data, index) in hajiUmrahData" :key="index">
        <td>{{ data.nama }}</td>
        <td>{{ data.hajiUmroh }}</td>
        <td>{{ data.tahun }}</td>
        <td>{{ data.tabungan }}</td>
      </tr>
    </tbody>
  </table>
</div>

  </div>
</template>

<script>
export default {
  data() {
  return {
    newVerse: '',
    quranVerses: [
      '"Allah SWT tidak bermaksud menyulitkan kamu, tetapi Dia bermaksud menyucikanmu dan menyempurnakan nikmat-Nya agar kamu bersyukur." (Quran 5:6)',
      '"Cinta pada Allah sama seperti cahaya terang. Tanpanya, kamu bagaikan terombang-ambing di lautan kegelapan'
    ],
    isHighlighted: false,
    fontSize: 16,
    hajiUmrahData: [],
    hajiUmroh: {
      nama: '',
      hajiUmroh: '', // Tambah properti hajiUmroh untuk menyimpan pilihan Haji/Umroh
      tahun: null,
      tabungan: null
    },
    // Opsi untuk pilihan Haji/Umroh
    hajiUmrohOptions: ['Umroh Biasa', 'Umroh Plus', 'Haji Biasa', 'Haji Plus']
  }
},

methods: {
  // Fungsi untuk menambahkan ayat Al-Qur'an baru
  addVerse() {
    // Periksa apakah input tidak kosong
    if (this.newVerse.trim()) {
      // Tambahkan ayat baru ke dalam daftar quranVerses
      this.quranVerses.push(this.newVerse.trim());
      // Kosongkan kembali input
      this.newVerse = '';
    }
  },
  removeVerse(index) {
    // Hapus ayat dari daftar berdasarkan indeks
    this.quranVerses.splice(index, 1);
  },
  toggleHighlight() {
    const element = document.querySelector('.example-element');
    
    // Toggle class 'highlighted'
    if (element.classList.contains('highlighted')) {
      element.classList.remove('highlighted');
    } else {
      element.classList.add('highlighted');
    }
  },
  toggleTextColor() {
    const element = document.querySelector('.example-element');
    
    // Toggle warna teks
    if (element.style.color === 'blue') {
      element.style.color = ''; // Reset ke warna default
    } else {
      element.style.color = 'blue'; // Ubah ke warna merah
    }
  },
  toggleFontSize() {
    const element = document.querySelector('.example-element');
    
    // Toggle font size
    const currentFontSize = parseInt(window.getComputedStyle(element).fontSize);
    if (currentFontSize === 35) {
      element.style.fontSize = '24px'; // Kurangi font size ke 14px
    } else {
      element.style.fontSize = '35px'; // Kembalikan font size ke 16px
    }
  },
  // Fungsi untuk submit data Haji dan Umrah
  submitHajiUmroh() {
    if (this.hajiUmroh.nama && this.hajiUmroh.hajiUmroh && this.hajiUmroh.tahun && this.hajiUmroh.tabungan) {
      this.hajiUmrahData.push({
        nama: this.hajiUmroh.nama,
        hajiUmroh: this.hajiUmroh.hajiUmroh, // Simpan pilihan Haji/Umroh
        tahun: this.hajiUmroh.tahun,
        tabungan: this.hajiUmroh.tabungan
      });
      this.hajiUmroh.nama = '';
      this.hajiUmroh.hajiUmroh = ''; // Set kembali pilihan Haji/Umroh ke nilai awal
      this.hajiUmroh.tahun = null;
      this.hajiUmroh.tabungan = null;
    }
  }
}
}
</script>

<style scoped>
/* CSS yang telah ada dipertahankan */
.container {
  max-width: 800px;
  margin: 0 auto;
  text-align: center; /* Mengatur konten ke tengah */
}

.highlighted {
  background-color: rgba(74, 116, 179, 0.958); /* Atur warna highlight sesuai keinginan */
}


.haji-umroh-container {
  text-align: left;
  margin-bottom: 20%;
  background-color: rgba(74, 116, 179, 0.778);
  padding: 40px 35px;
  border-radius: 10px;
  color: black;
}

.quran-container {
  border: #ffffff;
  border-radius: 10px;
  color: black;
  background-color: rgba(74, 116, 179, 0.778);
  padding: 30px 30px;
}

.haji-umroh-container h2 {
  text-align: center;
}

.header {
  margin-bottom: 20px;
}

.form-select {
  width: 103%;
  padding: 10px;
  border: 1px solid #ced4da;
  border-radius: 4px;
}

.form-input {
  width: 100%;
  padding: 10px;
  border: 1px solid #ced4da;
  border-radius: 4px;
}

.btn-submit {
  padding: 10px 20px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.btn-submit:hover {
  background-color: #0056b3;
}

.haji-umrah-table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}

.haji-umrah-table th,
.haji-umrah-table td {
  border: 1px solid #ced4da;
  padding: 8px;
  text-align: left;
}

.haji-umrah-table th {
  background-color: #f8f9fa;
}

.input-container {
  display: flex;
  margin-bottom: 20px;
}

.input-verse {
  flex: 1;
  padding: 10px;
  border: 1px solid #ced4da;
  border-radius: 4px;
  margin-right: 10px;
}

.btn-add {
  padding: 10px 20px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.btn-add:hover {
  background-color: #0056b3;
}

.quran-list {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

.quran-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  background-color: #fff;
  border: 1px solid #ced4da;
  border-radius: 4px;
  margin-bottom: 10px;
}

.btn-remove {
  padding: 5px 10px;
  background-color: #2c2e9d;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.btn-remove:hover {
  background-color: #c82333;
}

.example-element {
  padding: 20px;
  margin-bottom: 20px;
  border: 1px solid #ced4da;
  border-radius: 4px;
}

.button-group {
  display: flex;
  justify-content: center;
}

.btn-toggle,
.btn-increase {
  padding: 10px 20px;
  background-color: #225283;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.btn-toggle:hover,
.btn-increase:hover {
  background-color: #218838;
}

.form-group {
  margin-bottom: 20px;
}

.form-group label {
  display: block;
  margin-bottom: 5px;
}

.form-group input {
  width: 100%;
  padding: 10px;
  border: 1px solid #ced4da;
  border-radius: 4px;
}

.btn-submit {
  padding: 10px 20px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.btn-submit:hover {
  background-color: #0056b3;
}

.haji-umrah-table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}

.haji-umrah-table th,
.haji-umrah-table td {
  border: 1px solid #ced4da;
  padding: 8px;
  text-align: left;
}

.haji-umrah-table th {
  background-color: #f8f9fa;
}
</style>
