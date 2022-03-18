<template>
  <div class="header">
    <router-link to="/"><i class="icon fas fa-home"/></router-link>
  </div>
  <router-view/>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Libre+Barcode+128&display=swap');

html, body {
  margin: 0;
  height: 100%;
}
:root {
  --black-color: #000000;
  --dark-gray-color: #A9A5A2;
  --light-gray-color: #F3EFEB;
  --white-color: #FFFFFF;
  --dark-orange-color: #E28500;
  --orange-color: #F79201;
  --light-orange-color: #FDE4BF;
  --red-color: #EC4021;
  --green-color: #9CBE15;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  display: block;
  width: 100%;
  height: 100%;
  background-color: var(--light-gray-color);
}
.white { background-color: var(--white-color); }
.light-gray { background-color: var(--light-gray-color); }
.dark-gray { background-color: var(--dark-gray-color); }
.mb-1 { margin-bottom: 1em; }
.mb-half { margin-bottom: .5em; }
.mt-half { margin-top: .5em; }
.green { color: var(--green-color); }
.red { color: var(--red-color); }
.orange { color: var(--orange-color); }
.width-full { width: 100%; }
.noselect {
  -webkit-touch-callout: none; /* iOS Safari */
  -webkit-user-select: none; /* Safari */
  -khtml-user-select: none; /* Konqueror HTML */
  -moz-user-select: none; /* Old versions of Firefox */
  -ms-user-select: none; /* Internet Explorer/Edge */
  user-select: none; /* Non-prefixed version, currently
                                  supported by Chrome, Edge, Opera and Firefox */
}
button:active { background-color: var(--dark-orange-color) !important; }
</style>
<style scoped>
  .header {
    background-color: var(--orange-color);
    height: 3.5em;
    display: flex;
    justify-content: center;
    align-items: end;
    flex-direction: column;
    width: 100%;
    margin-bottom: 1em;
  }
  .icon {
    color: var(--white-color);
    font-size: 2em;
    margin-right: .5em;
  }
</style>
