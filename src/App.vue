<template>
  <div class="app">
<!--    <div class="nav">-->
<!--      <router-link to="/">Spacer</router-link>-->
<!--      <router-link to="/about">About</router-link>-->
<!--    </div>-->
    <router-view />
  </div>
</template>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;800&display=swap');
  *{
    box-sizing: border-box;
  }
  $gray-professional: rgba(62,77,87,1) !global;
  $vs-code-bg: rgba(33,33,33,1) !global;
  $iterm-bg: rgba(40,50,56,1) !global;
  $dark-blue-mac: rgba(25,30,50,1) !global;
  $purple-blue-grad: linear-gradient(135deg,#f403d1,#64b5f6) !global;
  $yellow-purpleish-grad: linear-gradient(135deg,#ffec61,#f321d7) !global;
  $green-blue-grad: linear-gradient(135deg,#24ff72,#2196f3) !global;
  $niceBoxShadow: 0px 0px 10px rgba(0, 0, 0, 0.56);
  $vue-color:  #2c3e50 !global;

  body {
    font-family: Montserrat, sans-serif;
    margin: 0;
    padding: 0;
  }
  .app{
    min-height: 100vh;
  }
</style>
