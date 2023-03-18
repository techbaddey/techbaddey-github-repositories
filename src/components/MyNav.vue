<template>
  <nav>
    <div class="profile">
      <router-link to="/">
        <img src="../assets/logo.png" alt="logo" />
      </router-link>
    </div>
    <div class="nav-items">
      <router-link class="layout-link" to="/">Profile</router-link>
      <router-link class="layout-link" to="/repositories"
        >Repositories</router-link
      >
      <router-link class="layout-link" to="/404">404</router-link>
    </div>
  </nav>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;
}

html,
body {
  scroll-behavior: smooth;
  background: #5c5e5f;
  overflow-x: hidden;
}

::-webkit-scrollbar {
  width: 3px;
}

nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 5;
  width: 100%;
  background: #24292e;
  color: #fff;
  padding: 10px 15px 4px 15px;
}

.profile img {
  width: 40px;
  height: 40px;
  border-radius: 50%;
}

.nav-items {
  display: flex;
  float: left;
  align-items: center;
  justify-content: center;
}

.layout-link {
  list-style: none;
  font-size: 1.2rem;
  padding: 5px 8px;
  cursor: pointer;
  text-decoration: none;
  color: #ff32ff;
  font-weight: 500;
  text-transform: uppercase;
  transition: 0.2s ease-in-out;
  margin-left: 1.5rem;
}

@media (max-width: 768px) {
  .layout-link {
    font-size: 0.9rem;
  }

  .layout-link {
  list-style: none;
  padding: 5px 8px;
  cursor: pointer;
  text-decoration: none;
  color: #ff32ff;
  font-weight: 500;
  text-transform: uppercase;
  transition: 0.2s ease-in-out;
  margin-left: 0.8rem;
}

}
</style>
