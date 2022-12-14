<template>
  <header>
    <div class="text-box">
      <h1>Reserva de computadores</h1>
      <p class="mt-3">Sistema para reserva de computadores na Fabrica de Software</p>
      <nuxt-link class="btn btn-outline btn-large btn-info" to="/login">Entrar no Sistema <span class="ml-2">&rarr;</span>
      </nuxt-link>
    </div>
  </header>
</template>

<script>
export default {
  head() {
    return {
      title: "Sistema de reservas"
    };
  },
};
</script>


<style>
header {
  min-height: 100vh;
  background-position: center;
  background-size: cover;
  position: relative;
}
.text-box {
  position: absolute;
  top: 50%;
  left: 10%;
  transform: translateY(-50%);
  color: black;
}
.text-box h1 {
  font-family: cursive;
  font-size: 5rem;
}
.text-box p {
  font-size: 2rem;
  font-weight: lighter;
}
</style>