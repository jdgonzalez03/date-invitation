<script setup>
import { ref } from 'vue'
import confetti from 'canvas-confetti'

const acceptInvitation = ref(false)

const accept = () => {
  acceptInvitation.value = true
  confetti()

  const audio = document.getElementById('song')
  audio.play()
  audio.play().catch(() => {
    console.log('El navegador ha bloqueado la reproducción automática')
  })
}

const close = () => {
  acceptInvitation.value = false
  const audio = document.getElementById('song')
  audio.pause()
}

const moveButton = (event) => {
  const button = event.target
  const app = document.getElementById('app')
  const appWidth = app.offsetWidth
  const appHeight = app.offsetHeight

  // Calcular nuevas posiciones aleatorias dentro del #app
  const newX = Math.random() * (appWidth - button.offsetWidth)
  const newY = Math.random() * (appHeight - button.offsetHeight)

  // Aplicar las nuevas posiciones
  button.style.position = 'absolute'
  button.style.left = `${newX}px`
  button.style.top = `${newY}px`
}
</script>

<template>
  <header>
    <h1>¿Quieres que comamos helados y de paso nos comamos?</h1>
  </header>

  <main class="button-container">
    <button class="yes-button" @click="accept">Si</button>
    <button class="no-button" @mouseover="moveButton" @touchend="moveButton">No</button>
  </main>

  <Teleport to="body">
    <div v-if="acceptInvitation" class="modal-overlay">
      <div class="modal-content">
        <p>
          Yo no perdono, porque el que perdona murió <br />
          en la cruz. Prepárate >:3
        </p>
        <strong>Nos vemos el martes</strong>
        <button class="close-button" @click="close">Cerrar</button>
      </div>
    </div>
  </Teleport>

  <audio id="song">
    <source src="../assets/audio-coqueto.mp3" type="audio/mpeg" />
  </audio>
  <footer>By <span>jdgonzalez03</span></footer>
</template>

<style>
body {
  background-color: #1e1e2f;
  color: #f0f0f0;
  font-family: 'Arial', sans-serif;
  margin: 0;
  padding: 0;
  min-height: 90vh;
}

h1 {
  color: #bb86fc;
  text-align: center;
  font-size: 2.4rem;
  margin-top: 20px;
}

footer {
  text-align: center;
  margin-top: 40px;
  font-size: 0.9rem;
  color: #9a9a9a;
}

footer span {
  color: #bb86fc;
  text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.4);
}

.button-container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 30px;
  position: relative;
  height: 200px;
}

/* Botón Si */
.yes-button {
  background-color: #624a9e;
  color: #fff;
  border: 5px solid #513d84;
  padding: 15px 30px;
  font-size: 1.2rem;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  margin-right: 20px;
}

.yes-button:hover {
  background-color: #513d84;
}

/* Botón No */
.no-button {
  background-color: #03dac6;
  color: #fff;
  border: 5px solid #01b4a3;
  padding: 15px 30px;
  font-size: 1.2rem;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  position: relative;
}

.no-button:hover {
  background-color: #01b4a3;
}

/* Estilos del modal */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 9999;
}

.modal-content {
  background: #2e2e3e;
  color: #fff;
  padding: 20px;
  border-radius: 10px;
  text-align: center;
  max-width: 300px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
}

.modal-content p {
  font-size: 1.2rem;
  margin-bottom: 10px;
}

.modal-content strong {
  display: block;
  margin-bottom: 20px;
  font-size: 1.1rem;
  color: #bb86fc;
}

/* Botón de cerrar */
.close-button {
  background-color: #624a9e;
  color: #fff;
  border: none;
  padding: 12px 25px;
  font-size: 1rem;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.close-button:hover {
  background-color: #513d84;
}
</style>
