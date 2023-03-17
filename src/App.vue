<template>
  <div id="app">
    <div class="loader-container" v-if="loading">
      <span class="loader"></span>
    </div>
    <div v-else>
      <router-view />
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      loading: true,
    };
  },
  mounted() {
    setTimeout(() => {
      this.loading = false;
    }, 3000);
  },
};
</script>

<style scoped>

.loader-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
.loader {
  width: 10rem;
  height: 10rem;
  display: inline-block;
  position: relative;
}
.loader::after,
.loader::before,
.loader span {
  content: "";
  box-sizing: border-box;
  width: 0.5rem;
  height: 0.5rem;
  border-radius: 50%;
  background-color: #ff3d00;
  position: absolute;
  left: 0;
  top: 0;
  animation: animloader 2s linear infinite;
}
.loader::after {
  animation-delay: 0.3s;
  left: 1.5rem;
}
.loader::before {
  animation-delay: 0.6s;
  left: 3rem;
}
.loader span {
  animation-delay: 0.9s;
  left: 4.5rem;
}
@keyframes animloader {
  0% {
    transform: scale(0);
    opacity: 1;
  }
  100% {
    transform: scale(1);
    opacity: 0;
  }
}
</style>
