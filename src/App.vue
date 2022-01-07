<template>
  <div>
    <h3 class="p-3 text-center">CloudAppi</h3>
    <create-user/>
    <get-user/>
  </div>
</template>

<script>
import GetUser from "./components/GetUser";
import CreateUser from "./components/CreateUser";

export default {
  name: "app",
  components: {
    GetUser,
    CreateUser,
  }
};
</script>
