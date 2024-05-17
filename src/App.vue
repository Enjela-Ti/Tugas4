<template>
  <div class="background">
    <img src="https://images.pexels.com/photos/20143271/pexels-photo-20143271/free-photo-of-kota-malam-bangunan-gedung.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1" />
  </div>
  <div class="Detail">
    <h1>Daftar Hotel</h1>
    <div class="Back">
      <div class="hotel-grid">
        <HotelItem 
          v-for="(hotel, index) in hotels" 
          :key="index" 
          :hotel="hotel" 
          @show-detail="showHotelDetail"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Swal from 'sweetalert2';
import HotelItem from './components/HotelItem.vue';

const hotels = ref([
  { name: 'Hotel Pangeran Pekanbaru', description: 'Jl. Jend. Sudirman No.371-373, Cinta Raja, Kec. Sail, Kota Pekanbaru, Riau 28126', amenities: ['WiFi', 'Kolam Renang', 'Spa'], imageUrl: 'https://bzpublishassets.blob.core.windows.net/media/assets_big/new-pool-and-balcony-8.webp' },
  { name: 'PRIME PARK Hotel', description: 'Alamat: Jl. Jend. Sudirman No.3 Blok A, Simpang Tiga, Kec. Bukit Raya, Kota Pekanbaru, Riau 28284.', amenities: ['WiFi', 'Pusat Kebugaran', 'Parkir Gratis'], imageUrl: 'https://static.promediateknologi.id/crop/0x0:0x0/0x0/webp/photo/riaupos/276-5-prime-park.gif' },
  { name: 'Ameera Hotel', description: 'Deskripsi Hotel C yang sangat panjang. Deskripsi Hotel C yang sangat panjang. Deskripsi Hotel C yang sangat panjang.', amenities: ['WiFi', 'Restoran', 'Bar'], imageUrl: 'https://ik.imagekit.io/tvlk/apr-asset/dgXfoyh24ryQLRcGq00cIdKHRmotrWLNlvG-TxlcLxGkiDwaUSggleJNPRgIHCX6/hotel/asset/10006704-ce9df15f08d9889e32c4c078e689f77b.jpeg?_src=imagekit&tr=c-at_max,h-280,q-40,w-412' },
  { name: 'Grand Zuri Hotel Pekanbaru', description: 'Deskripsi Hotel D yang sangat panjang. Deskripsi Hotel D yang sangat panjang. Deskripsi Hotel D yang sangat panjang.', amenities: ['WiFi', 'Kolam Renang', 'Spa'], imageUrl: 'https://ik.imagekit.io/tvlk/apr-asset/Ixf4aptF5N2Qdfmh4fGGYhTN274kJXuNMkUAzpL5HuD9jzSxIGG5kZNhhHY-p7nw/hotel/asset/10000621-940c6009718dfdf68b1400aed6b894ae.jpeg?tr=q-40,c-at_max,w-740,h-500&_src=imagekit' },
  { name: 'Aryaduta Pekanbaru', description: 'Alamat: Jl. Diponegoro No.34, Simpang Empat, Kec. Pekanbaru Kota, Kota Pekanbaru, Riau 28113', amenities: ['WiFi', 'Pusat Kebugaran', 'Parkir Gratis'], imageUrl: 'https://aryaduta-pekanbaru-hotel.hotelmix.id/data/Photos/OriginalPhoto/12839/1283944/1283944408/Aryaduta-Pekanbaru-Exterior.JPEG' },
  { name: 'The Premiere Hotel Pekanbaru', description: 'Alamat: Jl. Jend. Sudirman No.389, Simpang Empat, Kec. Pekanbaru Kota, Kota Pekanbaru, Riau 28121.', amenities: ['WiFi', 'Restoran', 'Bar'], imageUrl: 'https://media-cdn.tripadvisor.com/media/photo-s/0d/42/0a/ef/logo-depannya.jpg' },
  { name: 'Hotel Novotel Pekanbaru', description: 'Alamat: Jl. Riau No.59, Kp. Baru, Kec. Senapelan, Kota Pekanbaru, Riau 28154.', amenities: ['WiFi', 'Kolam Renang', 'Spa'], imageUrl: 'https://s-light.tiket.photos/t/01E25EBZS3W0FY9GTG6C42E1SE/t_htl-dskt/tix-hotel/images-web/2020/11/16/d43e6346-5ae4-4b5c-8d21-581d65301e6b-1605528213898-344cbf5d52ffb4369a92ca4e2e7c6ad7.jpg' },
  { name: 'Grand Jatra Hotel Pekanbaru', description: 'Berlokasi di: Mal Pekanbaru Alamat: Jl. Tengku Zainal Abidin No.1, Kota Tinggi, Kec. Pekanbaru Kota, Kota Pekanbaru, Riau 28116', amenities: ['WiFi', 'Pusat Kebugaran', 'Parkir Gratis'], imageUrl: 'https://lh3.googleusercontent.com/p/AF1QipNcOboOJzsPPsOtG2e1FfEz06eafZQe-nkao2ql=s1360-w1360-h1020' },
  { name: 'FOX Hotel Pekanbaru', description: 'Berlokasi di: Sadira Plaza Pekanbaru Alamat: Jl. Riau No.147, Padang Terubuk, Kec. Senapelan, Kota Pekanbaru, Riau 28154', amenities: ['WiFi', 'Restoran', 'Bar'], imageUrl: 'https://cf.bstatic.com/xdata/images/hotel/max500/82068562.jpg?k=82304e3fb99db8dfdc2d29e721dfc1aae859d380eec746e61e1948e0cb95364f&o=&hp=1' },
  { name: 'New Hollywood Hotel', description: 'Alamat: Jl. Kuantan Raya No.120, Sekip, Kec. Lima Puluh, Kota Pekanbaru, Riau 28151', amenities: ['WiFi', 'Kolam Renang', 'Spa'], imageUrl: 'https://ik.imagekit.io/tvlk/apr-asset/dgXfoyh24ryQLRcGq00cIdKHRmotrWLNlvG-TxlcLxGkiDwaUSggleJNPRgIHCX6/hotel/asset/10010793-84a505b6e40797202ee30236870e192a.jpeg?tr=q-40,c-at_max,w-740,h-500&_src=imagekit' },
  { name: 'Whiz Prime Hotel ', description: 'Alamat: Jl. Jend. Sudirman No.345, Sumahilang, Kec. Pekanbaru Kota, Kota Pekanbaru, Riau 28111', amenities: ['WiFi', 'Pusat Kebugaran', 'Parkir Gratis'], imageUrl: 'https://dynamic-media-cdn.tripadvisor.com/media/photo-o/17/02/ed/f3/whiz-hotel-sudirman-pekanbaru.jpg?w=300&h=-1&s=1' },
  { name: 'Amaris Hotel Pekanbaru', description: 'Alamat: Jalan KH. Wahid Hasyim Pinang Sebatang No.30, Sumahilang, Kec. Pekanbaru Kota, Kota Pekanbaru, Riau 28133', amenities: ['WiFi', 'Restoran', 'Bar'], imageUrl: 'https://lh3.googleusercontent.com/p/AF1QipNymupAEACaGcuqqzV-9GoPrN50P1SWo61_LHjs=s1360-w1360-h1020' }
]);

function showHotelDetail(hotel) {
  Swal.fire({
    title: hotel.name,
    html: `
      <div style="text-align: left;">
        <img src="${hotel.imageUrl}" alt="Foto Hotel" style="width: 100%; max-width: 400px; height: auto; object-fit: cover; border-radius: 8px; margin-bottom: 16px;">
        <p style="margin-bottom: 16px;">${hotel.description}</p>
        <h3 style="margin-bottom: 8px;">Fasilitas:</h3>
        <ul style="list-style-type: none; padding-left: 0;">
          ${hotel.amenities.map(amenity => `<li>${amenity}</li>`).join('')}
        </ul>
      </div>
    `,
    showCloseButton: true,
    showConfirmButton: false,
    customClass: {
      popup: 'custom-swal-popup',
      closeButton: 'custom-swal-close-button'
    }
  });
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto+Slab:wght@100..900&display=swap');
.Detail {
  margin-left: -100px;
}

.hotel-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 16px;
  color: black;
}

.custom-swal-popup {
  width: auto !important;
  max-width: 600px;
  text-align: center !important;
}

.custom-swal-close-button {
  color: #333 !important;
}

.Back {
  background-color: white;
  padding: 20px 50px;
  width: 100%;
  border-radius: 20px;
}

h1 {
  font-family: "Roboto Slab", serif;
  text-align: center;
  margin-bottom: 16px;
}
.background img{
  position: fixed;
  top: 0;
  left: 0;
  min-height: 90%;
  min-width: 1500px;
  width: 100%;
  height: 100%;
  overflow: hidden;
  z-index: -2;
  object-fit: cover;
  -webkit-background-size:cover; -moz-background-size:cover; -o-background-size:cover; background-size: cover;
  filter: brightness(0.8);
}
</style>
