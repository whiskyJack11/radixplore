<script >
import Form from './components/Form.vue';
import Map from './components/Map.vue'

export default {
  name: "app",
  components: {
    Form,
    Map
  },
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
    updateFormData(data) {
      console.log(data)
      this.formData = data
    }
  }
}
</script>

<template>
  <div class="app" >
    <div class="row" style="--bs-gutter-x: 0">
      <div class="col-lg-4 abc">
        <img class="logo" src="./assets/logo-x.png" />
        <hr style="margin: 0"/>
        <Form :update="updateFormData" :formData="formData"/>
      </div>
      <div class="col-lg-8">
        <Map :update="updateFormData" :formData="formData"/>
       </div>
    </div>
  </div>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
  
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }
  .app {
    /* padding: 1rem; */
    /* background: rgb(233, 250, 208); */
    height: 100vh;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
.logo {
      width: 100%;
      padding: 1.5rem 6rem;
}
.abc {
  overflow-y: auto;
    height: 100vh;
    overflow-x: hidden;
}
</style>
