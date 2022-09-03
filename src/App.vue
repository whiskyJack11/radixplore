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
        name: 'Test',
        description: 'User',
        latitude: '50.0',
        longitude: '90.0'
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
    <div class="row">
      <div class="col-lg-6">
        <Form :update="updateFormData"/>
      </div>
      <div class="col-lg-6">
        <Map :formData="formData"/>
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
    padding: 1rem;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
