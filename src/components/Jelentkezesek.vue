<template>
    <div>
      <h3>Jelentkezések</h3>
      <form @submit.prevent="registerTour">
        <div class="mb-3">
          <label for="email" class="form-label">Email</label>
          <input type="email" class="form-control" id="email" v-model="registration.email" required />
        </div>
        <div class="mb-3">
          <label for="groupSize" class="form-label">Csoport létszám</label>
          <input type="number" class="form-control" id="groupSize" v-model="registration.groupSize" required />
        </div>
        <div class="mb-3">
          <label for="tourSelect" class="form-label">Válasszon túrát</label>
          <select class="form-control" id="tourSelect" v-model="registration.tourId" required>
            <option v-for="tour in tours" :key="tour.id" :value="tour.id">{{ tour.nev }}</option>
          </select>
        </div>
        <button type="submit" class="btn btn-primary">Jelentkezés</button>
      </form>
  
      <ul class="list-group mt-3">
        <li
          v-for="registration in registrations"
          :key="registration.id"
          class="list-group-item d-flex justify-content-between align-items-center"
        >
          {{ registration.email }} - {{ registration.groupSize }} fő
          <button class="btn btn-danger" @click="deleteRegistration(registration.id)">Törlés</button>
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
          email: '',
          groupSize: '',
          tourId: '',
        },
        tours: [],
      };
    },
    methods: {
      async fetchTours() {
        try {
          const response = await fetch('http://your-backend-api/tours');
          const data = await response.json();
          if (response.ok) {
            this.tours = data;
          } else {
            alert('Failed to fetch tours');
          }
        } catch (error) {
          alert('Error: ' + error);
        }
      },
      async fetchRegistrations() {
        try {
          const response = await fetch('http://your-backend-api/registrations');
          const data = await response.json();
          if (response.ok) {
            this.registrations = data;
          } else {
            alert('Failed to fetch registrations');
          }
        } catch (error) {
          alert('Error: ' + error);
        }
      },
      async registerTour() {
        try {
          const response = await fetch('http://your-backend-api/registrations', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify(this.registration),
          });
          if (response.ok) {
            this.fetchRegistrations();
            this.registration = { email: '', groupSize: '', tourId: '' };
          } else {
            alert('Failed to register');
          }
        } catch (error) {
          alert('Error: ' + error);
        }
      },
      async deleteRegistration(id) {
        try {
          const response = await fetch(`http://your-backend-api/registrations/${id}`, {
            method: 'DELETE',
          });
          if (response.ok) {
            this.fetchRegistrations();
          } else {
            alert('Failed to delete registration');
          }
        } catch (error) {
          alert('Error: ' + error);
        }
      },
    },
    created() {
      this.fetchTours();
      this.fetchRegistrations();
    },
  };
  </script>
  