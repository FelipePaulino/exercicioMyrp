<template lang="pug">
table
    tr
      th Nome
      th Descrição
      th Prateleira
      th Galpão
      th Quantidade
      th Preço Unitário
      th Ações
      
    tr(v-for="(item, index) in itemList" :key="index")
      td {{ item.nome }}
      td {{ item.descricao }}
      td {{ item.prateleira }}
      td {{ item.galpao }}
      td {{ item.quantidade }}
      td {{ item.preco }}
      td
        button(@click="removeItem(index)") Remover
</template>

<script>
export default {
  props: {
    itemList: {
      type: Array,
      required: true,
    },
    removeItem: {
      type: Function,
      required: true,
    },
  },
};
</script>

<style scoped lang="scss">
table {
  width: 100%;
  border-collapse: collapse;
  margin-bottom: 20px;
  font-size: 16px;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

th,
td {
  border: 1px solid #ddd;
  padding: 15px;
  text-align: left;
  font-family: 'Playfair Display', serif;
}

th {
  background-color: #2196f3;
  color: white;
  font-weight: bold;
  font-family: 'Playfair Display', serif;
}

tr:nth-child(even) {
  background-color: #f2f2f2;
}

tr:hover {
  background-color: #ddd;
}

div {
  margin-top: 20px;
}

button {
  background-color: #2196f3;
  color: white;
  padding: 10px 15px;
  border: none;
  cursor: pointer;
  font-size: 16px;
  margin-right: 10px;
  font-family: 'Playfair Display', serif;
}

button:hover {
  background-color: #2196f3;
}


</style>
