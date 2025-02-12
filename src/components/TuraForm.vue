<template>
  <div class="card p-4">
    <h2>Új jelentkezés</h2>
    <select v-model="selectedTura" class="form-control mb-2">
      <option v-for="tura in turak" :key="tura.id" :value="tura.id">{{ tura.nev }}</option>
    </select>
    <input v-model="email" type="email" placeholder="Email" class="form-control mb-2" />
    <input v-model="letszam" type="number" placeholder="Létszám" class="form-control mb-2" />
    <button @click="addJelentkezes" class="btn btn-warning">Jelentkezés</button>
  </div>
</template>

<script>
export default {
  props: ["turak"],
  data() {
    return {
      selectedTura: "",
      email: "",
      letszam: 0
    };
  },
  methods: {
    async addJelentkezes() {
      await fetch('/api/jelentkezesek.php', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ tura_id: this.selectedTura, email: this.email, letszam: this.letszam })
      });
      this.$emit("update-jelentkezesek");
      this.email = "";
      this.letszam = 0;
    }
  }
};
</script>
