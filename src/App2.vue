<script>
export default {
  data() {
    return {
      name: 'ugesh simkhada',
      status: 'pendinadasdg',
      cars: ["honda", "tesla", "lamborgini", "toyota", "supra"],
      link: "https://ugeshsimkhada.com.np"
    };
  },
methods:{
  toggleStatus(){
    if (this.status === 'active') {
      this.status = 'pending';
    }else if(this.status === 'pending'){
      this.status = 'inactive';
    }else{
      this.status = 'active';
    }
  },
}
}
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">Use is active</p>
  <p v-else-if ="status === 'pending'">Use is pending</p>
  <p v-else>Use is inactive</p>
  <h5>List of Cars</h5>
  <ul>
    <li v-for="car in cars" :key="car">{{ car }}</li>
  </ul>
  <a v-bind:href="link">it'a a link</a>
  <br>
  <Button @click="toggleStatus">change status</Button>
</template>
