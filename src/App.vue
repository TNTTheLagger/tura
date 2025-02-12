<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Túrák</a>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav">
            <li class="nav-item">
              <a class="nav-link active" aria-current="page" href="#">Túrák</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#">Jelentkezések</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#">Kapcsolat</a>
            </li>
          </ul>
        </div>
      </div>
    </nav>
    <div class="container mt-5">
      <div class="row">
        <div class="col-md-6">
          <Turak />
        </div>
        <div class="col-md-6">
          <Jelentkezesek />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Turak from './components/Turak.vue';
import Jelentkezesek from './components/Jelentkezesek.vue';

export default {
  name: 'App',
  components: {
    Turak,
    Jelentkezesek
  }
};
</script>
