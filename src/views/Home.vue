<template>
  <div class="home">
    <h1><font-awesome-icon :icon="faCubes" size="2x" /></h1>
    <Main />
    <footer>
      Сделано <font-awesome-icon :icon="faCode" size="1x" /> на карантине @ayezum в 2020г.
    </footer>
  </div>
</template>

<script>
// @ is an alias to /src
import Main from "@/components/Main.vue";
/*import Jquery from "jquery";
let $ = Jquery;*/
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
//import { faBars } from "@fortawesome/free-solid-svg-icons";
import { faCode } from "@fortawesome/free-solid-svg-icons";
import { faCubes } from "@fortawesome/free-solid-svg-icons";

export default {
  name: "Home",
  components: {
    Main,
    FontAwesomeIcon
  },
  data() {
    return {
      faCode : faCode,
      faCubes : faCubes
      //faWindowClose: faWindowClose
    };
  }
};
</script>

<style scoped lang="scss">
  footer{
    /*bottom: 0;
    position: relative;
    margin: auto;
    left:50%;
    transform: translate(-50%,0);
    height: 50px;*/
  }
</style>