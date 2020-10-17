<template>
    <div id="map"></div>
    <div id="ui">
        <h1>Your coords</h1>
        <!-- <p> {{ coords.latitude }} Lat, {{ coords.longitude }} Long</p> -->
        <p> {{ coords.lat }} Lat, {{ coords.lng }} Long</p>
    </div>
</template>

<script>
const {Loader} = require('google-maps');

export default {
    data() {
        return {
            coords: {
                latitude: 0,
                longitude: 0
            },
        }
    },
    created() {
        const loader = new Loader('AIzaSyB1ijnYDZCZZ51sWfM7zxK2x7QwJLEeY8g', {});
        // const iconBase = "public/"
        if (navigator.geolocation) {
            navigator.geolocation.watchPosition(position => {
                this.coords = position.coords;
                this.coords = {lat: 25.061804, lng: 121.484142 };
                loader.load().then(function (google) {
                    // console.log(this.coords);
                    const map = new google.maps.Map(document.getElementById('map'), {
                        // center: {lat: position.coords.latitude, lng: position.coords.longitude},
                        center: {lat: 25.061804, lng: 121.484142 },
                        zoom: 17,
                    });
                    
                    const mark = new google.maps.Marker({
                        // position:  {lat: position.coords.latitude, lng: position.coords.longitude},
                        position:  {lat: 25.061804, lng: 121.484142 },
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
#ui {
    position: relative;
    z-index: 1;
    background-color: aliceblue;
    border: solid 1px;
    border-color: black;
}

</style>