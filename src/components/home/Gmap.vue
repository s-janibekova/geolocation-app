<template>
    <div class="map">
        <div class="google-map" id="map"></div>
    </div>
</template>

<script>
import firebase from 'firebase'
export default {
  name: 'Gmap',
  data () {
    return {
      lat: 43.3,
      lng: 77
    }
  },
  methods: {
    renderMap () {
      // eslint-disable-next-line
      const map = new google.maps.Map(document.getElementById('map'), {
        center: { lat: this.lat, lng: this.lng },
        zoom: 9,
        maxZoom: 15,
        minZoom: 3,
        streetViewControl: true
      })
    }
  },
  mounted () {
    this.renderMap()
    console.log(firebase.auth().currentUser)
  }
}
</script>

<style scoped>
  .google-map {
  width: 100%;
  height: 100%;
  margin: 0 auto;
  background: #fff;
  position: absolute;
  z-index: -1;
  top: 0;
  left: 0;
  }
</style>
