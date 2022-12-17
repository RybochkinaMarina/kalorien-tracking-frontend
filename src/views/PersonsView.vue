<template>
  <h1>Welcome to Persons</h1>
  <div class="container-fluid">
    <div class="row row-cols-1 row-cols-ad-4 g-4">
      <div class="col" v-for="person in persons" :key="person.id">
        <div class="card h=100">
          <img :src="getAvatar(person)" class="card-img-top" alt="person.firstName + ' ' + person.lastName">
          <div class="card-body">
            <h5 class="card-title">{{ person.firstName }} {{ person.lastName }}</h5>
            <p class="card-text">
              {{ person.firstName }} {{ person.lastName }} ist {{ person.vaccinated ? "geimpft" : "nicht geimpft"}} und
              hat {{ person.pets.length }} Haustiere.
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PersonsView',
  data () {
    return {
      persons: [
        // {
        //   id: 1,
        //   firstName: 'Max',
        //   lastName: 'Mustermann',
        //   vaccinated: true,
        //   gender: 'MALE',
        //   pets: []
        // },
        // {
        //   id: 2,
        //   firstName: 'Maxima',
        //   lastName: 'Meier',
        //   vaccinated: false,
        //   gender: 'FEMALE',
        //   pets: [
        //     1,
        //     2
        //   ]
        // }
      ]
    }
  },
  methods: {
    getAvatar (person) {
      if (person.gender === 'MALE') {
        return require('../assets/male.png')
      } else if (person.gender === 'FEMALE') {
        return require('../assets/female.png')
      }
    }
  },
  mounted () {
    // console.log('Hello World')
    const requestOptions = {
      method: 'GET',
      redirect: 'follow'
    }

    fetch('http://localhost:8080/api/v1/persons', requestOptions)
      .then(response => response.json())
      .then(result => console.log(result))
      .then(error => console.log('error', error))
  }
}
</script>

<style scoped>

</style>
