<template>
    <div>
      <h3>Jelentkezések</h3>
      <form @submit.prevent="register">
        <div class="mb-3">
          <label for="email" class="form-label">Email</label>
          <input type="email" class="form-control" v-model="registration.email" required />
        </div>
        <div class="mb-3">
          <label for="groupSize" class="form-label">Csoport létszám</label>
          <input type="number" class="form-control" v-model="registration.letszam" required />
        </div>
        <div class="mb-3">
          <label for="tourSelect" class="form-label">Túra kiválasztása</label>
          <select class="form-control" v-model="registration.tura_id" required>
            <option v-for="tour in tours" :key="tour.id" :value="tour.id">{{ tour.nev }}</option>
          </select>
        </div>
        <button type="submit" class="btn btn-primary">Jelentkezés</button>
      </form>
  
      <ul class="list-group mt-3">
        <li v-for="registration in registrations" :key="registration.id" class="list-group-item">
          {{ registration.email }} - {{ registration.letszam }} fő
          <button class="btn btn-danger btn-sm float-end" @click="deleteRegistration(registration.id)">Törlés</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        registrations: [],
        registration: {
          tura_id: '',
          email: '',
          letszam: '',
        },
        tours: [],
      };
    },
    methods: {
      async fetchRegistrations() {
        const response = await fetch('/api/jelentkezesek.php');
        const data = await response.json();
        this.registrations = data;
      },
      async fetchTours() {
        const response = await fetch('/api/turak');
        const data = await response.json();
        this.tours = data;
      },
      async register() {
        const response = await fetch('/api/jelentkezesek.php', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(this.registration),
        });
        if (response.ok) {
          this.fetchRegistrations();
          this.registration = { tura_id: '', email: '', letszam: '' };
        }
      },
      async deleteRegistration(id) {
        const response = await fetch(`/api/jelentkezesek.php?id=${id}`, {
          method: 'DELETE',
        });
        if (response.ok) {
          this.fetchRegistrations();
        }
      },
    },
    created() {
      this.fetchTours();
      this.fetchRegistrations();
    },
  };
  </script>
  