<template>
  <div class="container" :style="{ backgroundImage: 'url(' + image +')'  }">
    <div class="container__profile">
      <svg
        id="Layer_1"
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        x="0px"
        y="0px"
        viewBox="0 0 512 512"
        style="enable-background:new 0 0 512 512;"
        xml:space="preserve"
      >
        <g>
          <g>
            <path
              d="M333.187,237.405c32.761-23.893,54.095-62.561,54.095-106.123C387.282,58.893,328.389,0,256,0
                  S124.718,58.893,124.718,131.282c0,43.562,21.333,82.23,54.095,106.123C97.373,268.57,39.385,347.531,39.385,439.795
                  c0,39.814,32.391,72.205,72.205,72.205H400.41c39.814,0,72.205-32.391,72.205-72.205
                  C472.615,347.531,414.627,268.57,333.187,237.405z M164.103,131.282c0-50.672,41.225-91.897,91.897-91.897
                  s91.897,41.225,91.897,91.897S306.672,223.18,256,223.18S164.103,181.954,164.103,131.282z M400.41,472.615H111.59
                  c-18.097,0-32.82-14.723-32.82-32.821c0-97.726,79.504-177.231,177.231-177.231s177.231,79.504,177.231,177.231
                  C433.231,457.892,418.508,472.615,400.41,472.615z"
            />
          </g>
        </g>
      </svg>

      <div class="container__profile__text">
        <h2>{{name}}</h2>
        <button @click="modalStateOpen = true">Detail</button>
      </div>
    </div>
  </div>
  <teleport to="body">
    <div class="modal" :class="{'is-open': modalStateOpen}">
      <div class="modal-container">
        <div class="modal-left">
          <h1 class="modal-title">Playground</h1>
          <p>{{city}}</p>
          <p>{{street}}</p>
          <p>{{zip}}</p>
          <iframe
            width="300"
            height="170"
            frameborder="0"
            scrolling="no"
            marginheight="0"
            marginwidth="0"
            :src="'https://maps.google.com/maps?q='+ latitude +','+ longitude +'&hl=es&z=14&amp;output=embed'"
          ></iframe>
        </div>
        <div class="modal-right">
          <img :src="image" alt />
        </div>
        <button class="icon-button close-button" @click="modalStateOpen = false">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 50 50">
            <path
              d="M 25 3 C 12.86158 3 3 12.86158 3 25 C 3 37.13842 12.86158 47 25 47 C 37.13842 47 47 37.13842 47 25 C 47 12.86158 37.13842 3 25 3 z M 25 5 C 36.05754 5 45 13.94246 45 25 C 45 36.05754 36.05754 45 25 45 C 13.94246 45 5 36.05754 5 25 C 5 13.94246 13.94246 5 25 5 z M 16.990234 15.990234 A 1.0001 1.0001 0 0 0 16.292969 17.707031 L 23.585938 25 L 16.292969 32.292969 A 1.0001 1.0001 0 1 0 17.707031 33.707031 L 25 26.414062 L 32.292969 33.707031 A 1.0001 1.0001 0 1 0 33.707031 32.292969 L 26.414062 25 L 33.707031 17.707031 A 1.0001 1.0001 0 0 0 32.980469 15.990234 A 1.0001 1.0001 0 0 0 32.292969 16.292969 L 25 23.585938 L 17.707031 16.292969 A 1.0001 1.0001 0 0 0 16.990234 15.990234 z"
              stroke="white"
              fill="white"
            />
          </svg>
        </button>
      </div>
    </div>
  </teleport>
</template>

<script>
import { ref, toRefs } from 'vue';

export default {
  name: "PlaycardCard",
  props: ["playground"],
  setup(props) {
      const { playground } = toRefs(props);

      const name = ref("");
      const image = ref("");
      const modalStateOpen = ref(false);
      const city = ref("");
      const street = ref("");
      const zip = ref("");
      const latitude = ref("");
      const longitude = ref("");

      name.value = playground.value.name;
      image.value = playground.value.heroImage;
      city.value = playground.value.location.city;
      street.value = playground.value.location.street;
      zip.value = playground.value.location.zip;
      latitude.value = playground.value.location.latitude;
      longitude.value = playground.value.location.longitude;

      return {
        name,
        image,
        modalStateOpen,
        city,
        street,
        zip,
        latitude,
        longitude,
      }
  },
 };
</script>

<style>
.container {
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
  width: 350px;
  height: 500px;
  position: relative;
  box-shadow: 0 0 50px rgba(0, 0, 0, 0.315);
  margin: 25px;
}
.container .container__profile {
  background-color: #e4f2fd;
  display: flex;
  align-items: center;
  padding: 20px;
  position: absolute;
  right: 0;
  left: 0;
  bottom: 0;
}
.container .container__profile svg {
  width: 60px;
  height: 60px;
  border-radius: 50%;
  object-position: center;
  object-fit: cover;
  margin-right: 10px;
  border: 1px solid black;
}
.container .container__profile h2 {
  color: #334454;
  font-size: 1.2rem;
}
.container .container__profile p {
  color: #a1b2bc;
  font-size: 0.8rem;
}
.container .container__profile p b {
  font-style: italic;
}

.modal {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  height: 0px;
  background: rgba(51, 51, 51, 0.5);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  transition: 0.4s;
}
.modal-container {
  display: flex;
  max-width: 1024px;
  height: 768px;
  width: 100%;
  border-radius: 10px;
  overflow: hidden;
  position: absolute;
  opacity: 0;
  pointer-events: none;
  transition-duration: 0.3s;
  background: #fff;
  transform: translateY(100px) scale(0.4);
}
.modal-title {
  font-size: 26px;
  margin: 0;
  font-weight: 400;
  color: #55311c;
}
.modal-desc {
  margin: 6px 0 30px 0;
}
.modal-left {
  padding: 60px 30px 20px;
  background: #fff;
  flex: 1.5;
  transition-duration: 0.5s;
  transform: translateY(80px);
  opacity: 0;
}

.modal-right {
  flex: 2;
  font-size: 0;
  transition: 0.3s;
  overflow: hidden;
}
.modal-right img {
  width: 100%;
  height: 100%;
  transform: scale(2);
  -o-object-fit: cover;
  object-fit: cover;
  transition-duration: 1.2s;
}
.modal.is-open {
  height: 100%;
  background: rgba(51, 51, 51, 0.85);
}
.modal.is-open .modal-container {
  opacity: 1;
  transition-duration: 0.6s;
  pointer-events: auto;
  transform: translateY(0) scale(1);
}
.modal.is-open .modal-right img {
  transform: scale(1);
}
.modal.is-open .modal-left {
  transform: translateY(0);
  opacity: 1;
  transition-delay: 0.1s;
}
.modal-buttons {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.modal-buttons a {
  color: #fff;
  font-size: 14px;
}

.icon-button {
  outline: 0;
  position: absolute;
  right: 10px;
  top: 12px;
  width: 32px;
  height: 32px;
  border: 0;
  background: 0;
  padding: 0;
  cursor: pointer;
  color: #fff;
}

@media (max-width: 750px) {
  .modal-container {
    width: 90%;
  }

  .modal-right {
    display: none;
  }
}
</style>