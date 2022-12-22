<template>
  <div class="cards">
    <ProfileCard v-for="item in people"
                 :key=item.id
                 :info=item.url
    />
  </div>
</template>

<script>
import ProfileCard from './components/ProfileCard.vue'
import axios from 'axios'
import Token from '../delivery-methods'

export default {
  name: 'App',
  components: {
    ProfileCard
  },
  data() {
    return {
      people: null,
    }
  },
  created () {
    axios
        .get('https://api.github.com/users', {
          headers: {
            Authorization: 'Bearer ' + Token.token,
          }
        })
        .then(response => (this.people = response.data))
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.cards {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}
</style>
