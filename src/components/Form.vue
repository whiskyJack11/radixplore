<template>
    <div class="form">
        <input type="text" 
            v-model="editedFormData.name" 
            placeholder="Name"
        />
        <input type="text" 
            v-model="editedFormData.description"
            placeholder="Description" 
        />
        <input type="number" 
            v-model="editedFormData.latitude"
            placeholder="Latitude"
        />
        <input type="number" 
            v-model="editedFormData.longitude"
            placeholder="Longitude"
        />
        <button class="button-9" :disabled="!isFormValid" v-on:click="onSubmit">Find on map</button>
    </div>
</template>
<script>
export default {
    name: 'form',
    props: ["update", "formData"],
    data() {
        return {
            editedFormData: {
                name : this.formData.name,
                description : this.formData.description,
                latitude : this.formData.latitude,
                longitude : this.formData.longitude,
            }
        }
    },
    watch: { 
        formData() {
            this.editedFormData.name = this.formData.name;
            this.editedFormData.description = this.formData.description;
            this.editedFormData.latitude = this.formData.latitude;
            this.editedFormData.longitude = this.formData.longitude;
        }
    },
    computed: {
        isFormValid() {
            return this.editedFormData.name && this.editedFormData.description && this.editedFormData.latitude && this.editedFormData.longitude;
        }
    },
    methods: {
        onSubmit() {
            this.update(JSON.parse(JSON.stringify(this.editedFormData)));
        },
        clearForm() {
            this.update({})
        }
    }
}
</script>
<style scoped>
.form {
    padding: 3rem 2rem;
    display: flow-root;
}
input {
    width: 100%;
    margin: 0 0 1.5rem 0;
    padding: 0.4rem 0.8rem;
    font-family: monospace;
}
.button-9 {
  appearance: button;
  backface-visibility: hidden;
  background-color: #3a4eca;
  border-radius: 6px;
  border-width: 0;
  box-shadow: rgba(50, 50, 93, .1) 0 0 0 1px inset,rgba(50, 50, 93, .1) 0 2px 5px 0,rgba(0, 0, 0, .07) 0 1px 1px 0;
  box-sizing: border-box;
  color: #fff;
  cursor: pointer;
  /* font-family: -apple-system,system-ui,"Segoe UI",Roboto,"Helvetica Neue",Ubuntu,sans-serif; */
  font-size: 100%;
  height: 44px;
  line-height: 1.15;
  margin: 12px 0 0;
  outline: none;
  overflow: hidden;
  padding: 0 25px;
  position: relative;
  text-align: center;
  text-transform: none;
  transform: translateZ(0);
  transition: all .2s,box-shadow .08s ease-in;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  /* width: 100%; */
  float: right;
  font-family: monospace;
}

.button-9:disabled {
  cursor: default;
  background-color: grey;


}

.button-9:focus {
  box-shadow: rgba(50, 50, 93, .1) 0 0 0 1px inset, rgba(50, 50, 93, .2) 0 6px 15px 0, rgba(0, 0, 0, .1) 0 2px 2px 0, rgba(50, 151, 211, .3) 0 0 0 4px;
}

.button-6 {
  align-items: center;
  background-color: #FFFFFF;
  border: 1px solid rgba(0, 0, 0, 0.1);
  border-radius: .25rem;
  box-shadow: rgba(0, 0, 0, 0.02) 0 1px 3px 0;
  box-sizing: border-box;
  color: rgba(0, 0, 0, 0.85);
  cursor: pointer;
  display: inline-flex;
  font-family: system-ui,-apple-system,system-ui,"Helvetica Neue",Helvetica,Arial,sans-serif;
  font-size: 16px;
  font-weight: 600;
  justify-content: center;
  line-height: 1.25;
  margin: 0;
  min-height: 3rem;
  padding: calc(.875rem - 1px) calc(1.5rem - 1px);
  position: relative;
  text-decoration: none;
  transition: all 250ms;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  vertical-align: baseline;
  width: auto;
}

.button-6:hover,
.button-6:focus {
  border-color: rgba(0, 0, 0, 0.15);
  box-shadow: rgba(0, 0, 0, 0.1) 0 4px 12px;
  color: rgba(0, 0, 0, 0.65);
}

.button-6:hover {
  transform: translateY(-1px);
}

.button-6:active {
  background-color: #F0F0F1;
  border-color: rgba(0, 0, 0, 0.15);
  box-shadow: rgba(0, 0, 0, 0.06) 0 2px 4px;
  color: rgba(0, 0, 0, 0.65);
  transform: translateY(0);
}
</style>