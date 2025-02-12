<template>
  <div class="container">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        <img src="./assets/logo.png" alt="Logo" class="logo" />
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item"><a class="nav-link" href="#">Túrák</a></li>
          <li class="nav-item"><a class="nav-link" href="#">Jelentkezések</a></li>
          <li class="nav-item"><a class="nav-link" href="#">Kapcsolat</a></li>
        </ul>
      </div>
    </nav>

    <div class="row">
      <div class="col-md-6">
        <h2>Új túra hozzáadása</h2>
        <form @submit.prevent="addTura">
          <div class="mb-3">
            <label class="form-label">Túra neve</label>
            <input type="text" class="form-control" v-model="newTura.nev" required />
          </div>
          <div class="mb-3">
            <label class="form-label">Táv (km)</label>
            <input type="number" class="form-control" v-model.number="newTura.tav" min="1" required />
          </div>
          <div class="mb-3">
            <label class="form-label">Elérhető helyek száma</label>
            <input type="number" class="form-control" v-model.number="newTura.elerheto_hely" min="1" required />
          </div>
          <button class="btn btn-warning">Hozzáadás</button>
        </form>
      </div>
      <div class="col-md-6">
        <h2>Rögzített túrák</h2>
        <ul class="list-group">
          <li class="list-group-item d-flex justify-content-between align-items-center" v-for="tura in turak" :key="tura.id">
            {{ tura.nev }} - {{ tura.tav }} km
            <button class="btn btn-warning">Részletek</button>
          </li>
        </ul>
      </div>
    </div>

    <div class="mt-5">
      <h2>Új jelentkezés</h2>
      <form @submit.prevent="submitJelentkezes">
        <div class="mb-3">
          <label class="form-label">Túra kiválasztása</label>
          <select class="form-control" v-model="selectedTura">
            <option v-for="tura in turak" :key="tura.id" :value="tura.id">{{ tura.nev }}</option>
          </select>
        </div>
        <div class="mb-3">
          <label class="form-label">Email</label>
          <input type="email" class="form-control" v-model="email" required />
        </div>
        <div class="mb-3">
          <label class="form-label">Létszám</label>
          <input type="number" class="form-control" v-model.number="resztvevok" min="1" required />
        </div>
        <button class="btn btn-warning">Jelentkezés</button>
      </form>
    </div>
    
    <div class="mt-5">
      <h2>Rögzített jelentkezések</h2>
      <ul class="list-group">
        <li class="list-group-item d-flex justify-content-between align-items-center" v-for="jelentkezes in jelentkezesek" :key="jelentkezes.id">
          {{ jelentkezes.tura }} - {{ jelentkezes.email }} ({{ jelentkezes.resztvevok }} fő)
          <button class="btn btn-warning">Törlés</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      turak: [],
      jelentkezesek: [],
      newTura: { nev: '', tav: 1, elerheto_helyek: 1 },
      selectedTura: null,
      email: '',
      resztvevok: 1
    };
  },
  mounted() {
    this.fetchTurak();
    this.fetchJelentkezesek();
  },
  methods: {
    async fetchTurak() {
      let response = await fetch('/api/turak.php');
      this.turak = await response.json();
    },
    async fetchJelentkezesek() {
      let response = await fetch('/api/jelentkezesek.php');
      this.jelentkezesek = await response.json();
    },
    async addTura() {
      await fetch('/api/turak.php', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(this.newTura)
      });
      this.fetchTurak();
    },
    async submitJelentkezes() {
      await fetch('/api/jelentkezesek.php', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
          tura_id: this.selectedTura,
          email: this.email,
          resztvevok: this.resztvevok
        })
      });
      this.fetchJelentkezesek();
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
