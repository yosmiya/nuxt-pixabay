<template>
  <div>
    <Header />
    <transition name="page" mode="out-in">
      <Nuxt />
    </transition>
  </div>
</template>

<style>
.page-enter-active,
.page-leave-active {
  transition: opacity 1s;
}
.page-enter,
.page-leave-active {
  opacity: 0;
}
</style>