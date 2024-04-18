<template>
  <AppLayout />
  <div class="repos-container">
    <span class="loader" v-if="loading"></span>
    <div class="repos" :style="{ opacity: loading ? 0.5 : 1 }" v-else>
      <h1>Oyinkansola Shoroye's Repositories</h1>
      <ul>
        <li
          style="text-transform: uppercase"
          v-for="repo in paginatedRepositories"
          :key="repo.id"
        >
          🚀
          <router-link
            class="links"
            :to="{ name: 'single-repo', params: { id: repo.id } }"
            >{{ repo.name }}</router-link
          >
        </li>
      </ul>
      <div class="btn-container">
        <button
          @click="currentPage--"
          :disabled="currentPage === 1"
          :class="{ disabled: currentPage === 1 }"
        >
          Prev
        </button>
        <span>Page {{ currentPage }} of {{ totalPages }}</span>
        <button
          @click="currentPage++"
          :disabled="currentPage === totalPages"
          :class="{ disabled: currentPage === totalPages }"
        >
          Next
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import AppLayout from "./MyNav.vue";

export default {
  name: "AllRepos",
  components: {
    AppLayout,
  },
  data() {
    return {
      repositories: [],
      currentPage: 1,
      perPage: 7,
      totalPages: 0,
      loading: true,
    };
  },
  methods: {
    async fetchRepositories() {
      this.loading = true;
      try {
        await new Promise((resolve) => setTimeout(resolve, 1000));
        const response = await axios.get(
          "https://api.github.com/users/techbaddey/repos"
        );
        this.repositories = response.data;
        this.totalPages = Math.ceil(this.repositories.length / this.perPage);
      } catch (error) {
        console.error(error);
      } finally {
        this.loading = false;
      }
    },
  },
  computed: {
    paginatedRepositories() {
      const startIndex = (this.currentPage - 1) * this.perPage;
      const endIndex = startIndex + this.perPage;
      return this.repositories.slice(startIndex, endIndex);
    },
  },
  mounted() {
    this.fetchRepositories();
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Space+Mono&display=swap");

.repos-container {
  margin-top: 135px;
  margin-bottom: 40px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.repos {
  width: 50%;
  margin: -3rem auto 0 auto;
  padding: 1rem;
  background-color: #24292e;
  border-radius: 10px;
  box-shadow: 0 0 10px 0 rgba(0, 0, 0, 0.2);
  opacity: 1;
  transition: opacity 0.5s ease-in-out;
}

.loader-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
.loader {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  position: relative;
  animation: rotate 1s linear infinite;
}
.loader::before,
.loader::after {
  content: "";
  box-sizing: border-box;
  position: absolute;
  inset: 0px;
  border-radius: 50%;
  border: 5px solid #a79595;
  animation: prixClipFix 2s linear infinite;
}
.loader::after {
  border-color: #ff32ff;
  animation: prixClipFix 2s linear infinite, rotate 0.5s linear infinite reverse;
  inset: 6px;
}
@keyframes rotate {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
@keyframes prixClipFix {
  0% {
    clip-path: polygon(50% 50%, 0 0, 0 0, 0 0, 0 0, 0 0);
  }
  25% {
    clip-path: polygon(50% 50%, 0 0, 100% 0, 100% 0, 100% 0, 100% 0);
  }
  50% {
    clip-path: polygon(50% 50%, 0 0, 100% 0, 100% 100%, 100% 100%, 100% 100%);
  }
  75% {
    clip-path: polygon(50% 50%, 0 0, 100% 0, 100% 100%, 0 100%, 0 100%);
  }
  100% {
    clip-path: polygon(50% 50%, 0 0, 100% 0, 100% 100%, 0 100%, 0 0);
  }
}

h1 {
  color: #fff;
  text-align: center;
  font-size: 1.5rem;
  font-family: "Space Mono", monospace;
  margin-bottom: 20px;
  text-decoration: underline;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
}

li {
  font-family: "Space Mono", monospace;
  font-size: 1.2rem;
  margin: 0.3rem 0;
  padding: 1rem;
  border-radius: 10px;
}

li:hover {
  background-color: #1a1e22;
  transform: scale(1.02);
}

.pagination {
  display: flex;
  justify-content: center;
  margin-top: 1rem;
}

.links {
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}

.links:visited {
  color: #ff32ff;
}

.btn-container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 2rem 0 1.5rem 0;
}

.btn-container span {
  color: #fff;
}

button {
  background-color: #ff32ff;
  color: #fff;
  border: none;
  padding: 0.5rem 2rem;
  border-radius: 5px;
  margin: 0 0.7rem;
  font-size: 1.2rem;
}

.disabled {
  background-color: #1a1e22;
  color: #fff;
  cursor: not-allowed;
}

@media (max-width: 768px) {
  .repos {
    width: 80%;
  }
  h1 {
    font-size: 1.5rem;
  }

  li {
    font-size: 1rem;
  }

  button {
    font-size: 1rem;
  }
}
</style>
