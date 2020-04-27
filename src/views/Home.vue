<template>
  <div class="home">
    <h1><img src="~@/assets/img/title-img.png" alt="Чакроанализ"></h1>
    <Main />
    <footer>
      <!--Сделано <font-awesome-icon :icon="faCode" size="1x" /> на карантине @ayezum в 2020г.-->
    </footer>
  </div>
</template>

<script>
// @ is an alias to /src
import Main from "@/components/Main.vue";
/*import Jquery from "jquery";
let $ = Jquery;*/
//import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
//import { faBars } from "@fortawesome/free-solid-svg-icons";
//import { faCode } from "@fortawesome/free-solid-svg-icons";

export default {
  name: "Home",
  components: {
    Main
    //FontAwesomeIcon
  },
  data() {
    return {
      //faCode : faCode
      //faWindowClose: faWindowClose
    };
  }
};
</script>
<style scoped lang="scss">
h1{
  color: #fff;
  margin-bottom: 20px;
  text-align: center;
  img{
    margin-top: 20px;
    width: auto;
    height: 170px;
  }
}
</style>