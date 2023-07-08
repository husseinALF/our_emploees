<script setup>
import EmployeeList from "./components/EmployeeList.vue";
import Title from "./components/Title.vue";
</script>

<template>
  <Title />
  <EmployeeList />
</template>

<style>
body {
  background: linear-gradient(
    0deg,
    rgba(34, 193, 195, 1) 0%,
    rgba(253, 187, 45, 1) 100%
  );

  height: 100dvh;
}
</style>
