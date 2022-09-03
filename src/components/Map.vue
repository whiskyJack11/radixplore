<template>
    <div class="map">
        <h2>Map</h2>
        <div id="map">
            
        </div>
    </div>
</template>
<script>
export default {
    name: 'map',
    props: ["formData"],
    data() {
        return {
            map: null,
            marker: null
        }
    },
    computed: {
        latLng() {
            return [this.formData.latitude, this.formData.longitude]
        }
    },
    watch: {
        latLng() {
            this.setLocation()
        }
    },
    methods: {
        setMap() {
            this.map = L.map('map').setView([-31.95, 115.86], 13);
            L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
                maxZoom: 19,
                attribution: '© OpenStreetMap'
            }).addTo(this.map);
        },
        setLocation() {
            if (this.marker == null) {
                console.log(this.formData.name + '<br>' + this.formData.description)
                this.marker = L.marker(this.latLng).addTo(this.map)
            } else {
                this.marker.setLatLng(this.latLng).update();
            }

            this.marker.bindPopup(this.formData.name + '<br>' + this.formData.description)

            this.map.setView(this.latLng);
        }
    },

    mounted() {
        this.setMap()
    }
}
</script>
<style scoped>
#map {
    height: 300px;
    padding: 1rem;
}
.map {
    
    padding: 1rem;;
}

</style>