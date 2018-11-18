<template>
  <div class="map">
    
    
    <div class="center" style="padding-top:15vh;">
        <gmap-map
        :center="center"
        :zoom="14"
        style="width:50vw;  height: 60vh; margin-left: 25%;"
        >
        <gmap-marker
            :key="index"
            v-for="(m, index) in markers"
            :position="m.position"
            @click="center=m.position"
        ></gmap-marker>
        </gmap-map>
    </div>
  </div>
</template>

<script>
import firebase from 'firebase'
export default {
  name: "GoogleMap",
  data() {
    return {
      // default to Montreal to keep it simple
      // change this to whatever makes sense
      center: { lat: 7.007430, lng: 100.502060 },
      markers: [    {
              position:{ lat: 7.007451, lng: 100.5000493 }

          },{
              position:{ lat:7.0066264, lng: 100.4996118 }

          },{
              position:{ lat: 6.9985061, lng: 100.4970043 }

          },{
              position:{ lat: 6.997792, lng: 100.4966737 }

          },{
              position:{ lat: 6.9988287, lng: 100.4976601 }

          }],
      places: [],
      currentPlace: null
    };
  },

  mounted() {
    this.geolocate();
  },

  methods: {
    // receives a place object via the autocomplete component
    setPlace(place) {
      this.currentPlace = place;
    },
    geolocate: function() {
      navigator.geolocation.getCurrentPosition(position => {
        this.center = {
          lat: position.coords.latitude,
          lng: position.coords.longitude
        };
      });
    },
    logout: function () {
      firebase.auth().signOut().then(() => {
        this.$router.replace('login')
      })
    }
  }
};
</script>

<style scoped>
.map {
    background-color: aliceblue;
    height: 100vh;
}
.menu:hover{
  color: white;
}
.active a{
font-weight: bold;
}
a{
  font-size: 30px;
}
</style>
