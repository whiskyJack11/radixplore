<template>
    <div class="form">
        <h2>Enter location details</h2>
        <label>Name</label>
        <input type="text" v-model="formData.name" />
        <label>Description</label>
        <input type="text" v-model="formData.description" />
        <label>Latitude</label>
        <input type="number" v-model="formData.latitude"/>
        <label>Longitude</label>
        <input type="number" v-model="formData.longitude"/>
        <button v-on:click="onSubmit">Submit</button>

    </div>
</template>
<script>
export default {
    name: 'form',
    props: ["update"],
    data() {
        return {
            formData: {
                name: '',
                description: '',
                latitude: '',
                longitude: ''
            }
        }
    },
    methods: {
        onSubmit() {
            this.update(JSON.parse(JSON.stringify(this.formData)));
        }
    }
}
</script>
<style scoped>
.form {
    padding: 1rem;
}
input {
    width: 100%;
    margin: 0 0 1rem 0;
}
button {
  background-color: #4CAF50; /* Green */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
}
</style>