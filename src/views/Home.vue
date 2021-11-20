<template>
  <div class="home">
    <Header />
    <Form />
    <Footer />
  </div>
</template>

<script>
// @ is an alias to /src
import Header from "@/components/Header.vue";
import Form from "@/components/Form.vue";
import Footer from "@/components/Footer.vue";

export default {
  name: "Home",
  components: {
    Header,
    Form,
    Footer,
  },
};
</script>
