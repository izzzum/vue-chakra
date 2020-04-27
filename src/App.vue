<template>
  <div id="app">
    <router-view />
  </div>
</template>

<style lang="scss">
@mixin font-face($name, $format, $formatName, $type, $filename) {
  @font-face {
    font-family: $name;
    src:  local($name), url("~@/assets/fonts/#{$filename}.#{$format}") format('#{$formatName}');
    font-weight: $type;
    font-style: $type;
  }
}
@include font-face('Open Sans Condensed', 'ttf', 'truetype', 'bold', 'OpenSansCondensed-Bold');
@include font-face('Open Sans Condensed', 'ttf', 'truetype', 'normal', 'OpenSansCondensed-Light');
#app {
  font-family: 'Open Sans Condensed', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100vh;
  font-size: 16px;
}
body, html, #app{
  background-color: #f3f5fd;
  width: 100%;
  overflow-x: hidden;
}
input {
  background: #f5f6ff !important;
}
</style>
