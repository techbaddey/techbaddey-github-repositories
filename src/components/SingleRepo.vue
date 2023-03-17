<template>
  <div class="repos-container">
    <span class="loader" v-if="loading"></span>
    <div class="repos" v-else>
      <h1>{{ repository.name }}</h1>
      <p class="desc">{{ repository.description }}</p>
      <hr class="rule" />
      <p class="rep"><strong>Language:</strong> {{ repository.language }}</p>
      <p class="rep">
        <strong>Visibility:</strong> {{ repository.visibility }}
      </p>
      <p class="rep"><strong>Created:</strong> {{ repository.created_at }}</p>
      <p class="rep">
        <strong>Last Updated:</strong> {{ repository.updated_at }}
      </p>
      <p class="rep url">
        <strong>URL: </strong>
        <a class="links" :href="repository.html_url">
          {{ repository.html_url }}</a
        >
      </p>
      <p class="rep">
        <strong>Stars:</strong> {{ repository.stargazers_count }}
      </p>
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

<style>
.repos h1 {
  text-align: center;
  text-transform: uppercase;
  font-size: 1.5rem;
  margin: 1rem 0;
}
.btn {
  display: flex;
  justify-content: center;
  align-items: center;
  border: none;
  color: white;
  padding: 10px 16px;
  text-decoration: none;
  font-size: 16px;
  margin: 4px auto;
  cursor: pointer;
}

.rep {
  font-size: 1.2rem;
  margin: 1.5rem 0;
}

.desc {
  font-size: 1.2rem;
  text-align: justify;
}

.rule {
  border: 0;
  height: 1px;
  background-image: linear-gradient(to right, #c3cfe2, #e1e6ee);
}

.url {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  word-wrap: break-word;
}

@media (max-width: 768px) {
  .repos-container {
    margin-left: -1rem;
  }
}
</style>
