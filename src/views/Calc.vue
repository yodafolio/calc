<template>
  <v-app>
    <v-main>
      <Calculator />
    </v-main>
  </v-app>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Calculator from '@/components/Calculator.vue';

@Component({
  components: {
    Calculator,
  },
})
export default class extends Vue {}
</script>

<style scoped></style>
