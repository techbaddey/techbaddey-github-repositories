<template>
  <div class="repos-container">
    <span class="loader" v-if="loading"></span>
    <div class="repos" v-else>
      <div class="head">
        <h1>
          <a :href="repository.html_url"> 🔗 {{ repository.name }} </a>
        </h1>
        <p class="rep" title="repo visibility">
          🌎︎ {{ repository.visibility }}
        </p>
      </div>

      <p class="desc" title="repo description">{{ repository.description }}</p>

      <div class="foot">
        <p class="rep" title="repo language">{{ repository.language }}</p>
        <p class="rep" title="stars count">
          ★ {{ repository.stargazers_count }}
        </p>
        <p class="rep" title="watchers count">
          👁 {{ repository.watchers_count }}
        </p>
        <p class="rep" title="repo size">{{ repository.size }}KB</p>
      </div>
      <button @click="redirectToHome" class="btn">Back</button>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      repository: {},
      loading: true,
    };
  },
  async created() {
    await new Promise((resolve) => setTimeout(resolve, 1000));

    const response = await fetch(
      `https://api.github.com/repositories/${this.$route.params.id}`
    );
    const data = await response.json();
    this.repository = data;
    this.loading = false;
  },
  methods: {
    redirectToHome() {
      this.$router.push("/repositories");
    },
  },
  mounted() {},
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Space+Mono&display=swap");

.repos-container .repos {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 85%;
  background: #000;
  padding: 1rem;
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
}

.head {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-family: "Space Mono", monospace;
  color: #fff;
}

.foot {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-family: "Space Mono", monospace;
}

.foot p {
  font-family: "Space Mono", monospace;
}

.repos h1 {
  text-transform: uppercase;
  font-size: 1.3rem;
  margin: 1rem 0;
  font-family: "Space Mono", monospace;
  color: #fff;
}

.repos a {
  text-decoration: none;
  color: #fff;
  font-family: "Space Mono", monospace;
}

.repos p {
  font-family: "Space Mono", monospace;
}
.btn {
  display: flex;
  justify-content: center;
  align-items: center;
  border: none;
  color: white;
  padding: 5px 8px;
  text-decoration: none;
  font-size: 16px;
  margin: 4px auto;
  cursor: pointer;
  background-color: #24292e;
}

.rep {
  font-size: 1.2rem;
  margin: 1.5rem 0;
  color: white;
}

.desc {
  font-size: 1.2rem;
  text-align: justify;
  color: #8a8b8b;
}

@media screen and (min-width: 768px) {
  .repos-container .repos {
    width: 35%;
  }
}
</style>
