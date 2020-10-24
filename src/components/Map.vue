<template>
    <div id="map"></div>
    <Searchbar class="searchbar"/>
    <div v-if="showinfo">
        <PlaceInfo class="info" :place="placemarker"/>
    </div>
</template> 

<script>
const {Loader} = require('google-maps');
import Searchbar from './Searchbar.vue'
import PlaceInfo from './PlaceInfo.vue'

export default {
    components: {
        Searchbar,
        PlaceInfo
    },
    prop: {
        },
    data() {
        return {
            showinfo: false,
            placemarker: {
                position: {
                    lat: Number, 
                    lng: Number
                },
                icon: String,
                title: String,
            },  
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
                const that = this
                loader.load().then(function (google) {
                    const map = new google.maps.Map(document.getElementById('map'), {
                        center: {lat: position.coords.latitude, lng: position.coords.longitude},
                        // center: {lat: 25.061804, lng: 121.484142 },
                        zoom: 12,
                    });
                    
                    const marker = new google.maps.Marker({
                        position:  {lat: 25.061762, lng: 121.484143},
                        icon: "https://i.imgur.com/QtyZUwk.png",
                        map,
                        title: 'unpackaged.U商店',
                    });
                    const infowindow = new google.maps.InfoWindow({
                        content: "hello world",
                    });

                    marker.addListener('click', () => {
                        infowindow.open(marker.get("map"), marker);
                        that.placemarker = {
                            position: marker.position,
                            icon: marker.icon,
                            title: marker.title
                        }
                        that.showinfo = true
                    })
                });
            })
        }else{ 
            console.log("Geolocation is not supported by this browser");
        }
    },
    methods: {

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
.searchbar {
    position: relative;
    z-index: 1;
    background-color: #00994f;
    border: solid 3px;
    border-color: #FDFDFD;
    margin-top: 60px;
    margin-right: 50%;
    text-align: left;
}

.info, #temp {
    position: relative;
    z-index: 1;
    background-color: #00994f;
    border: solid 3px;
    border-color: #FDFDFD;
    margin-top: 160px;
    margin-right: 50%;
    text-align: left;
}

@media screen and (max-width: 769px) {
    #searchbar {
        margin-right: auto;
    }
}

</style>