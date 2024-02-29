<template lang="pug">
header
  .logo-container
    img(src="/imagens/logo.png", alt="Logo da Empresa")
  .valores
    div
      p Total de Itens: {{ totalItems }}
    div
      p Preço Total: {{ formatCurrency(totalPrice) }}
</template>
  
<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  methods: {
    formatCurrency(value: number): string {
      return new Intl.NumberFormat("pt-BR", {
        minimumFractionDigits: 2,
        maximumFractionDigits: 2,
      }).format(value);
    },
  },
  props: {
    totalItems: Number,
    totalPrice: Number,
  },
});
</script>
  
  <style scoped lang="scss">
header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background-color: #2962ff;
  color: white;
  padding: 10px;
  text-align: center;

  img {
    width: 30%;
  }

  .logo-container {
    display: flex;
    align-items: center;
    padding: 20px;
  }

  .valores {
    display: flex;
    flex-direction: column;
    margin-right: 70px;
  }

  p {
    text-align: left;
    font-family: "Playfair Display", serif;
    font-size: 18px;
  }
}
</style>
  