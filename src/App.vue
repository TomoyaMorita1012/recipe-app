<template>
  <div id="nav">
    <!-- アプリケーションのタイトル -->
    <div class="title">
      <div class="app-title">
        <h1>今日のご飯は何にする？？？</h1>
      </div>
    </div>
    <!-- routerセクション -->
    <div class="routing_sec">
      <router-link to="/">レシピを探す</router-link>
      <span> or </span>
      <router-link to="/ranking">ランキングを見る</router-link>
    </div>
  </div>
  <router-view />
</template>

<script></script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Potta+One&display=swap");

/* 背景画像指定 */
body:before {
  content: "";
  display: block;
  position: fixed;
  top: 0;
  left: 0;
  z-index: -1;
  width: 100%;
  height: 100vh;
  background: url(~@/assets/app-bg.jpg) center no-repeat;
  background-size: 90%;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  word-break: break-all;
}
p {
  font-weight: bold;
}
.title {
  /* タイトル外枠 */
  width: 70%;
  margin: 0 auto 20px;
  padding: 30px 20px;
  background-color: #fff;
  border-radius: 80px;
}
.app-title {
  /* タイトル内枠 */
  width: 60%;
  margin: 10px auto;
  padding: 5px;
  border-radius: 50px;
  background-color: #fda128c2;
  color: #fff;
  font-family: "Potta One", cursive;
  font-weight: normal;
  font-size: 18px;
}

#nav {
  /* router部 */
  margin: 10px;
  padding: 30px;
  font-family: "Potta One", cursive;
}
#nav a {
  color: #b97828;
  font-size: 26px;
  text-decoration: none;
}
#nav a.router-link-exact-active {
  color: #ff9100;
  font-size: 36px;
}

form {
  /* form全体 */
  width: 60%;
  margin: 40px auto;
  text-align: center;
  display: flex;
  justify-content: center;
  align-items: center;
}
.form_style {
  border: none;
  background-color: #fcc277c2;
  padding: 25px 5px;
  box-shadow: 3px 10px 10px #cc9d60, -3px 10px 10px #cc9d60;
  border-radius: 10px;
}
label {
  flex-grow: 1;
  color: #000;
  font-family: "Potta One", cursive;
  font-size: 20px;
  display: inline-block;
  width: 150px;
  margin: 10px;
}
.look_btn {
  flex-grow: 1;
  width: 20%;
  height: 50px;
  color: #000;
  font-family: "Potta One", cursive;
  font-size: 18px;
  background-color: #fff;
  border: 2px solid #ff6666;
  border-radius: 5px;
  padding: 5px 15px;
  margin-top: 10px;
  transition-duration: 1s;
}
.look_btn:hover {
  transform: scale(1.1);
  background: #ff6666;
  font-weight: bold;
  color: #fff;
}
.look_btn:hover:after {
  content: " →";
}
select {
  flex-grow: 2;
  width: 300px;
  height: 30px;
}

button {
  margin: 10px;
}
a:active {
  color: #000;
}

@media screen and (max-width: 1200px) {
  body:before {
    background-image: url(~@/assets/mobile-bg.jpg);
    background-size: cover;
  }
  .app-title {
    width: 80%;
  }
  .look_btn {
    width: 35%;
  }
}
@media screen and (max-width: 960px) {
  .title {
    width: 80%;
    border-radius: 90px;
  }
  .app-title {
    border-radius: 60px;
  }
  form {
    display: inline-block;
    width: 70%;
    margin: 20px auto;
  }
  label {
    display: block;
    margin: 10px auto 15px;
  }
  select {
    display: block;
    margin: 10px auto;
  }
}
@media screen and (max-width: 680px) {
  body:before {
    background-image: url(~@/assets/phone-bg.jpg);
    background-size: cover;
  }
  #nav a {
    display: block;
  }
  .routing_sec > span {
    display: block;
  }
  .title {
    width: 90%;
    border-radius: 100px;
  }
  .app-title {
    border-radius: 70px;
  }
  select {
    width: 70%;
  }
  .look_btn {
    width: 55%;
  }
}
@media screen and (max-width: 380px) {
  #nav {
    padding: 20px;
  }
  .title {
    padding: 30px 15px;
  }
  .app-title {
    width: 90%;
    padding: 5px;
    font-size: 16px;
  }
  #nav a {
    font-size: 20px;
  }
  #nav a.router-link-exact-active {
    font-size: 28px;
  }
  form {
    width: 80%;
  }
  select {
    width: 80%;
  }
  .look_btn {
    width: 70%;
    font-size: 16px;
  }
}
@media screen and (max-width: 290px) {
  #nav {
    padding: 0;
  }
  .title {
    padding: 30px 10px;
  }
  .app-title {
    width: 80%;
  }
}
</style>
