<template>
    <div class="map">
        <div id="map">  
        </div>
    </div>
</template>
<script>
export default {
    name: 'map',
    props: ["update", "formData"],
    data() {
        return {
            map: null,
            marker: null
        }
    },
    computed: {
        latLng() {
            if (this.formData.latitude && this.formData.longitude) {
                return [this.formData.latitude, this.formData.longitude]
            } else {
                null
            }
        }
    },
    watch: {
        latLng() {
            console.log(this.latlng)
            if (this.latLng == null) {
                if (this.marker != null) {
                    this.map.removeLayer(this.marker)
                    this.marker = null;
                }
                this.map.setView(['0.0','0.0'], 0)
            } else {
                this.setLocation();
            }
        }
    },
    methods: {
        setMap() {
            this.map = L.map('map').setView([-31.95, 115.86], 13);
            L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
                maxZoom: 19,
                attribution: '© OpenStreetMap'
            }).addTo(this.map);

            this.map.setGeocoder('Nominatim', {});
		    let searchControl = L.esri.Geocoding.geosearch().addTo(this.map);
            searchControl.on('results', this.onSearchResult);

            // const response  = this.map.addControl(L.control.search());
            // console.log(response);
        },
        onSearchResult(data) {
            try {
                let location = data.results[0];
                this.update(
                    {
                    name: location.properties.PlaceName,
                    description: location.properties.LongLabel,
                    latitude: location.latlng.lat.toFixed(2),
                    longitude: location.latlng.lng.toFixed(2)
                }
                );
            } catch(error) {
                this.update(
                    {
                        name: '',
                        description: '',
                        latitude: '',
                        longitude: ''
                    }
                )
            }
            
        },
        setLocation() {
            if (this.marker == null) {
                this.marker = L.marker(this.latLng).addTo(this.map)
            } else {
                this.marker.setLatLng(this.latLng).update();
            }

            this.marker.bindPopup(this.formData.name + '<br>' + this.formData.description)

            this.map.setView(this.latLng, 13);
        }
    },

    mounted() {
        this.setMap()
    }
}
</script>
<style scoped>
#map {
    height: 100vh;
    /* padding: 1rem; */
}
.map {
    
    /* padding: 1rem;; */
}

</style>