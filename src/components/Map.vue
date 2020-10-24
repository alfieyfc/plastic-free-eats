<template>
    <div id="map"></div>
    <Searchbar id="searchbar"/>
    <div id="ui" v-if="dev">
        <h1>Your coords</h1>
        <!-- <p> {{ coords.latitude }} Lat, {{ coords.longitude }} Long</p> -->
        <p> {{ coords.lat }} Lat, {{ coords.lng }} Long</p>
    </div>
</template>

<script>
const {Loader} = require('google-maps');
import Searchbar from './Searchbar.vue'

export default {
    components: {
        Searchbar
    },
    data() {
        return {
            dev: false,
            coords: {
                latitude: 0,
                longitude: 0
            },
        }
    },
    created() {
        const loader = new Loader(process.env.VUE_APP_API, {});
        if (navigator.geolocation) {
            navigator.geolocation.watchPosition(position => {
                this.coords = position.coords;
                this.coords = {lat: 25.061804, lng: 121.484142 };
                loader.load().then(function (google) {
                    const map = new google.maps.Map(document.getElementById('map'), {
                        center: {lat: position.coords.latitude, lng: position.coords.longitude},
                        // center: {lat: 25.061804, lng: 121.484142 },
                        zoom: 17,
                    });
                    
                    const mark = new google.maps.Marker({
                        position:  {lat: 25.061762, lng: 121.484143 },
                        icon: "https://i.imgur.com/QtyZUwk.png",
                        map,
                        title: "unpackaged.U°Ó©±",
                    });
                    console.log(mark)
                });
            })

        }else{ 
            console.log("Geolocation is not supported by this browser");
        }
    }
}
</script>

<style scoped>
#map {
    position: absolute;
    height: 100%;
    width: 100%;
    top: 0;
    left: 0;
    z-index: 0;
}
#searchbar, #ui {
    position: relative;
    z-index: 1;
    background-color: #00994f;
    border: solid 3px;
    border-color: #FDFDFD;
    margin-top: 60px;
    margin-right: 50%;
    text-align: left;
}

@media screen and (max-width: 769px) {
    #searchbar {
        margin-right: auto;
    }
}

</style>