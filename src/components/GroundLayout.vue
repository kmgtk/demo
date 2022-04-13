<template>
  <div class="Ground">
    <Header />
    <h1>{{connectData}}</h1>
    <Memo />
    <Footer />
  </div>

</template>

<script>

import Header from "@/components/HeaderLayout.vue";
import Footer from "@/components/FooterLayout.vue";
import Memo from "@/components/MemoLayout.vue"
export default {

  components: {Header, Footer, Memo},

};
</script>
