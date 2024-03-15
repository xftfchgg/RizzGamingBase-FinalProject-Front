<script setup>

import axios from 'axios';
import VueCookies from 'vue-cookies'

const postData = {
  account:"123",
  password:"123",
};
var id = "CfDJ8KshjrWbZT1IhORnLUROfOWil0YgDOa5HHu40VyBeZ6KcCbRX0qfEfb-bFO8Se6sTyoVKejoA_s3GadZgXzD8jEINj9hc8KInS4YOswfxRmnNKt6vK4sgp7abfJGkHJ_Ng";

axios.post('https://localhost:7048/api/Members/Login', postData)
  .then(response => {
  
    if(response.data[0]=="登入成功"){
      // 設置 'account' Cookie，過期時間為一小時後
      id= response.data[1]
      VueCookies.set('accountId', response.data[1], new Date(Date.now() + 3600000)); // 3600000 毫秒 = 1 小時
      console.log(response.data[0]);

    }
    else{
      console.log(response.data[0]);
    }
  })
  .catch(error => {
    console.log(error);
  });

axios.post(`https://localhost:7048/api/Members/MemberId?protectId=${id}`, id)
  .then(response => {
    console.log(response.data);
  })
  .catch(error => {
    console.log(error);
});
</script>

<template>
  
  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh; 
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
