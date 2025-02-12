<template>
    <div>
      <h3>Túrák</h3>
      <ul class="list-group">
        <li
          v-for="tour in tours"
          :key="tour.id"
          class="list-group-item d-flex justify-content-between align-items-center"
        >
          {{ tour.nev }} - {{ tour.tav }} km
          <button class="btn btn-info" @click="toggleDetails(tour.id)">Részletek</button>
          <div v-if="showDetails[tour.id]" class="mt-2">
            <p>Helyek: {{ tour.elerheto_hely }}</p>
          </div>
        </li>
      </ul>
  
      <form @submit.prevent="addTour">
        <div class="mb-3">
          <label for="tourName" class="form-label">Név</label>
          <input type="text" class="form-control" id="tourName" v-model="newTour.nev" required />
        </div>
        <div class="mb-3">
          <label for="tourDistance" class="form-label">Távolság</label>
          <input type="number" class="form-control" id="tourDistance" v-model="newTour.tav" required />
        </div>
        <div class="mb-3">
          <label for="availableSeats" class="form-label">Elérhető helyek</label>
          <input type="number" class="form-control" id="availableSeats" v-model="newTour.elerheto_hely" required />
        </div>
        <button type="submit" class="btn btn-primary">Hozzáadás</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        tours: [],
        newTour: {
          nev: '',
          tav: '',
          elerheto_hely: '',
        },
        showDetails: {},
      };
    },
    methods: {
      async fetchTours() {
        const response = await fetch('/api/turak');
        const data = await response.json();
        this.tours = data;
      },
      async addTour() {
        const response = await fetch('/api/turak', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(this.newTour),
        });
        if (response.ok) {
          this.fetchTours();
          this.newTour = { nev: '', tav: '', elerheto_hely: '' };
        }
      },
      toggleDetails(tourId) {
        this.showDetails[tourId] = !this.showDetails[tourId];
      },
    },
    created() {
      this.fetchTours();
    },
  };
  </script>
  