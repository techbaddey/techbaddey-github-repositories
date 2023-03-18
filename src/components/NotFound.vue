<template>
  <div class="page-404">
    <div class="page-404__inner">
      <p class="first-text">Oops!</p>
      <p class="second-text">
        We can't seem to find the page you're looking for.
      </p>
      <p class="third-text">Error code: 404</p>
      <p class="fourth-text">Here are some helpful links instead:</p>
      <div class="link-container">
        <router-link class="link" to="/">Profile</router-link>
        <router-link class="link" to="/repositories">Repositories</router-link>
        <router-link class="link" to="/404">404</router-link>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "NotFound",
};
</script>

<style scoped>

.page-404 {
  height: 100%;
  width: 100%;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  background-color: #1a1e22;
}

.first-text {
  font-size: 100px;
  color: #fff;
}

.second-text {
  font-size: 23px;
  color: #8a8b8b;
  margin-bottom: 3rem;
}

.third-text {
  font-size: 16px;
  color: #8a8b8b;
  margin-bottom: 3rem;
}

.fourth-text {
  font-size: 16px;
  color: #fff;
  margin-bottom: 0.1rem;
}

.link-container .link {
  font-size: 16px;
  color: #ff32ff;
  margin-bottom: 0.5rem;
  text-decoration: underline;
  margin-right: 1rem;
}
</style>
