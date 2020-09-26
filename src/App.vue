<template lang="pug">
  v-app
    Calc
</template>

<script>
export default {
  name: 'App',
  components: {
    Calc: () => import('@/components/Calc'),
  },
  data: () => ({
    //
  }),
};
</script>
