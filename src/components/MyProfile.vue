<template>
  <AppLayout />
  <div class="home">
    <div class="container">
      <div class="content">
        <div class="img">
          <img :src="profile.avatar_url" />
        </div>
        <h1>{{ profile.name }}</h1>
        <p class="login">@{{ profile.login }}</p>
        <p class="bio">{{ profile.bio }}</p>

        <div class="follows">
          <div class="followings"><b>35</b> <br />Repositories</div>
          <div class="followers">
            <b>{{ profile.followers }}</b> <br />Followers
          </div>
        </div>

        <a :href="profile.html_url" target="_blank"
          ><button>View on GitHub</button></a
        >
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import AppLayout from "./MyNav.vue";

export default {
  name: "HomePage",
  components: {
    AppLayout,
  },
  data() {
    return {
      profile: " ",
    };
  },

  created: function () {
    axios
      .get("https://api.github.com/users/teqbaddie")
      .then((response) => {
        this.profile = response.data;
      })
      .catch((error) => {
        console.log(error);
      });
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Space+Mono&display=swap");

.home {
  height: 100vh;
  width: 100%;
  background: #1a1e22;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  margin-top: 50px;
}

h1 {
  text-align: center;
  font-weight: 500;
  font-size: 2.4rem;
  color: #fff;
}

img {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0 auto;
  border: 0.35rem solid #ff32ff;
  width: 220px;
  border-radius: 50%;
  margin-bottom: 1.15rem;
  transition: opacity 0.3s ease;
}

.content .login {
  text-align: center;
  font-weight: 500;
  font-size: 1.3rem;
  color: #06fbfa;
  margin-bottom: 2px;
  cursor: pointer;
  font-family: "Space Mono", monospace;
}

.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  margin: 0 auto;
}

.content .bio {
  color: #fff;
  max-width: 100%;
  font-size: 1.1rem;
  text-align: center;
  padding: 0px 10px;
}

.content .follows {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 25px;
  margin-bottom: 35px;
  color: #fff;
}

.content .follows .followers {
  padding: 10px 20px;
  background-color: #24292e;
  border-radius: 8px;
  text-align: center;
  margin-left: 20px;
}

.content .follows .followings {
  padding: 10px 20px;
  background-color: #24292e;

  border-radius: 8px;
  text-align: center;
}

a {
  text-decoration: none;
}

.content button {
  background: #ff32ff;
  margin: 0 auto;
  display: flex;
  justify-content: center;
  align-items: center;
  text-decoration: none;
  cursor: pointer;
  margin-bottom: 20px;
  font-weight: 500;
}
</style>
