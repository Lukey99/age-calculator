<template>
  <div id="app">
    <h1>Hello</h1>
  </div>
</template>

<script>
export default {
  name: "App",
};
</script>

<style lang="scss">
@font-face {
  font-family: "Poppins";
  src: url("./assets/fonts/poppins-regular-webfont.woff2") format("woff2"),
    url("./assets/fonts/poppins-regular-webfont.woff") format("woff");
  font-weight: normal;
  font-style: normal;
}

@font-face {
  font-family: "Poppins-Bold";
  src: url("./assets/fonts/poppins-bold-webfont.woff2") format("woff2"),
    url("./assets/fonts/poppins-bold-webfont.woff") format("woff");
  font-weight: bold;
  font-style: normal;
}

@font-face {
  font-family: "Poppins-BoldItalic";
  src: url("./assets/fonts/poppins-bolditalic-webfont.woff2") format("woff2"),
    url("./assets/fonts/poppins-bolditalic-webfont.woff") format("woff");
  font-weight: bold;
  font-style: italic;
}

@font-face {
  font-family: "Poppins-ExtraBoldItalic";
  src: url("./assets/fonts/poppins-extrabolditalic-webfont.woff2") format("woff2"),
    url("./assets/fonts/poppins-extrabolditalic-webfont.woff") format("woff");
  font-weight: bolder;
  font-style: italic;
}

/* Utilisez votre police dans d'autres sélecteurs CSS */
body {
  font-family: "Poppins-ExtraBoldItalic", sans-serif;
}

* {
  margin: 0;
  padding: 0;
  left: 0;
  top: 0;
}

:root {
  --white: hsl(0, 0%, 100%);
  --off-white: hsl(0, 0%, 94%);
  --light-grey: hsl(0, 0%, 86%);
  --smockey-grey: hsl(0, 1%, 44%);
  --off-black: hsl(0, 0%, 8%);
}

#app {
  width: 100vw;
  height: 100vh;
  background: var(--off-white);
}
</style>
