<template>
  <div>
<!--    header    -->
    <Header />
<!--    main    -->
    <div style="display: flex">
<!--      aside    -->
      <Aside />
<!--      router view     -->
      <router-view style="flex: 1"/>

    </div>
  </div>

</template>

<style>

</style>

<script>
import Header from "@/components/Header";
import Aside from "@/components/Aside";

export default {
  name: "Layout",
  components:{
    Aside,
    Header
  }
}
</script>
