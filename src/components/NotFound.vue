<template>
   <div class="page-404">
    <div class="page-404__inner">
      <h1> Oops! </h1>
      <p> We can't seem to find the
page you're looking for. </p>
      <p>Error code: 404</p>
      <p>Here are some helpful links instead:</p>
      <div class="link-container">
      <!-- <RouterLink to="/" class="link"> Go Home </RouterLink> -->
      <router-link class="layout-link" to="/">Profile</router-link>
      <router-link class="layout-link" to="/repositories">Repositories</router-link>
      <router-link class="layout-link" to="/404">404</router-link>
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
  display: flex;
  justify-content: center;
  align-items: center;
  
  /* Mobile Styles */
  @media screen and (max-width: 600px) {
    flex-direction: column;
  }
}


.page-404__inner {
  width: 75%;
  text-align: center;
  
  /* Mobile Styles */
  @media screen and (max-width: 600px) {
    width: 100%;
  }
}

</style>
