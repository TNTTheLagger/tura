<template>
  <div class="container">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        <img src="./assets/logo.png" alt="Logo" class="logo" />
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item"><a class="nav-link" href="#" @click="activeTab = 'turak'">Túrák</a></li>
          <li class="nav-item"><a class="nav-link" href="#" @click="activeTab = 'jelentkezes'">Jelentkezések</a></li>
          <li class="nav-item"><a class="nav-link" href="#" @click="activeTab = 'kapcsolat'">Kapcsolat</a></li>
        </ul>
      </div>
    </nav>

    <TuraForm v-if="activeTab === 'turak'" @update-turak="fetchTurak" />
    <JelentkezesForm v-if="activeTab === 'jelentkezes'" :turak="turak" @update-jelentkezesek="fetchJelentkezesek" />
  </div>
</template>

<script>
import TuraForm from "@/components/TuraForm.vue";
import JelentkezesForm from "@/components/JelentkezesForm.vue";

export default {
  components: {
    TuraForm,
    JelentkezesForm
  },
  data() {
    return {
      turak: [],
      activeTab: 'turak'
    };
  },
  mounted() {
    this.fetchTurak();
  },
  methods: {
    async fetchTurak() {
      let response = await fetch('/api/turak.php');
      this.turak = await response.json();
    },
    async fetchJelentkezesek() {
      let response = await fetch('/api/jelentkezesek.php');
      this.jelentkezesek = await response.json();
    }
  }
};
</script>

<style>
.logo {
  width: 100px;
  margin-right: 20px;
}
</style>
