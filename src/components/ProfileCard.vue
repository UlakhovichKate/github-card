<template>
  <div class="ui card">
    <div class="image">
      <img :src=about.avatar_url :alt=about.name>
    </div>
    <div class="content">
      <a :href=about.url class="header" target="_blank">{{ about.name }}</a>
      <div class="meta">
        <span class="date">Joined in {{ about.created_at }}</span>
      </div>
      <div class="description">
        {{ about.bio }}
      </div>
    </div>
    <div class="extra content">
      <a>
        <i class="user icon"></i>
        {{ about.followers }} {{ countFriends() }}
      </a>
    </div>
  </div>
</template>

<script>
  import axios from "axios";
  import Token from '../../delivery-methods'

  export default {
    name: "ProfileCard",
    props: {
      info: String
    },
    data() {
      return {
        about: null,
        ava: null
      }
    },
    methods: {
      countFriends() {
        return Number(this.about.followers) === 1 ? 'Friend' : 'Friends';
      },
    },
    created () {
      axios
          .get(this.info, {
            headers: {
              Authorization: 'Bearer ' + Token.token,
            }
          })
          .then(response => (this.about = response.data))
    }
  }
</script>

<style scoped>

</style>
