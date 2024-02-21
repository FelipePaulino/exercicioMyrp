<template lang="pug">
div
    Header(:totalItems="totalItems", :totalPrice="totalPrice")
    div
      .container
        .buttonAdd
          .formContent
            button(v-if="!showForm", @click="toggleForm") Adicionar Novo Item
          
          .form
            div(v-if="showForm")
              form(@submit.prevent="addItem")
                label(for="nome") Nome
                input#nome(v-model="newItem.nome", type="text", required)

                label(for="descricao") Descrição
                input#descricao(v-model="newItem.descricao", type="text", required)

                label(for="prateleira") Prateleira
                input#prateleira(v-model="newItem.prateleira", type="text", required)

                label(for="galpao") Galpão
                input#galpao(v-model="newItem.galpao", type="text", required)

                label(for="quantidade") Quantidade
                input#quantidade(v-model="newItem.quantidade", type="number", required)
                
                label(for="preco") Preço
                input#preco(v-model="newItem.preco", type="number", step="0.02", required)
  
                div 
                  .buttonAddCancel
                    button(type="submit") Adicionar
                    button(v-if="showForm", @click="cancelAdd") Cancelar
      Table(:itemList="itemList", :removeItem="removeItem")
</template>
  
<script>
  import dados from "./dados.json";
  import Header from "./components/Header.vue";
  import Table from "./components/Table.vue";
  
  export default {
    components: {
      Header,
      Table,
    },
  
    data() {
      return {
        itemList: [],
        newItem: {
          nome: "",
          descricao: "",
          prateleira: null,
          galpao: "",
          quantidade: null,
          preco: null,
        },
        showForm: false,
      };
    },
  
    computed: {
      totalItems() {
        return this.itemList.reduce((total, item) => total + item.quantidade, 0);
      },
      totalPrice() {
        return this.itemList.reduce((total, item) => total + item.preco * item.quantidade , 0).toFixed(2);
      },
    },
  
    methods: {

      showRemoveFeedback() {
      this.showAlert("Item removido com sucesso!", "alert-success");
    },
  
      removeItem(index) {
      this.itemList.splice(index, 1);
      this.showRemoveFeedback();
    },
      addItem() {
        const trimmedNome = this.newItem.nome.trim();
        const trimmedDescricao = this.newItem.descricao.trim();
        const trimmedPrateleira = this.newItem.prateleira.trim();
        const trimmedGalpao = this.newItem.galpao.trim();
  
        if (
          trimmedNome &&
          trimmedDescricao &&
          trimmedPrateleira &&
          trimmedGalpao &&
          this.newItem.quantidade !== null &&
          this.newItem.preco !== null
        ) {
          this.itemList.push({ ...this.newItem });
          this.newItem = {
            nome: "",
            descricao: "",
            prateleira: null,
            galpao: "",
            quantidade: null,
            preco: null,
          };
          this.showForm = false;
          this.showAlert("Item adicionado com sucesso!", "alert-success");
        } else {
          this.showAlert("Por favor, preencha todos os campos corretamente.", "alert-warning");
        }
      },
  
      toggleForm() {
        this.showForm = !this.showForm;
      },
      cancelAdd() {
        this.newItem = {
          nome: "",
          descricao: "",
          prateleira: null,
          galpao: "",
          quantidade: null,
          preco: null,
        };
        this.showForm = false;
        this.$refs.itemForm.reset(); 
      },
  
      fetchData() {
        setTimeout(() => {
          this.itemList = dados;
        }, 1000);
      },
  
      showAlert(message, type) {
        const alertClass = `alert ${type}`;
        const alertElement = document.createElement("div");
        alertElement.className = alertClass;
        alertElement.textContent = message;
  
        const closeButton = document.createElement("button");
        closeButton.textContent = "Fechar";
        closeButton.addEventListener("click", () => {
          document.body.removeChild(alertElement);
        });
  
        alertElement.appendChild(closeButton);
        document.body.appendChild(alertElement);
      },
    },
  
    mounted() {
      this.fetchData();
    },
  };
</script>
  
  <style lang="scss">
  
  .container{
    margin-top: 70px;
    margin-left: 20px;
  }
  
  .formContent{
    margin-top: 230px;
    margin-left: 20px;
  }
  
  .buttonAdd button {
    font-family: 'Playfair Display', serif;
    background-color: #2196f3;
    color: white;
    padding: 10px 15px;
    border: none;
    cursor: pointer;
    font-size: 16px;
    margin-right: 10px;
  }
  
  .buttonAdd button:hover {
    background-color: #2196f3;
  }
  
  div {
    margin-top: 20px;
  }
  
  h2 {
    font-size: 20px;
    margin-bottom: 10px;
    font-family: 'Playfair Display', serif;
  }
  
  label {
    display: block;
    margin-bottom: 5px;
    font-family: 'Playfair Display', serif;
  }
  
  input {
    width: 50%;
    padding: 10px;
    margin-bottom: 10px;
    box-sizing: border-box;
    font-family: 'Playfair Display', serif;
  }
  
  button {
    font-family: 'Playfair Display', serif;
    background-color: #2196f3;
    color: white;
    padding: 10px 15px;
    border: none;
    cursor: pointer;
    font-size: 16px;
    margin-right: 10px;
    margin-bottom: 20px;
  }
  
  button:hover {
    background-color: #2196f3;
  }
  
  header {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    background-color: #2962ff;
    color: white;
    padding: 10px;
    text-align: center;
  }
  
  .alert {
    font-family: 'Playfair Display', serif;
    position: fixed;
    top: 10px;
    left: 50%;
    transform: translateX(-50%);
    background-color: #f44336;
    color: white;
    padding: 15px;
    margin-bottom: 20px;
    border-radius: 8px;
    font-size: 16px;
    text-align: center;
    z-index: 1000;
  }
  
  .alert-success {
    background-color: #4CAF50;
    font-family: 'Playfair Display', serif;
  }
  
  .alert button {
    font-family: 'Playfair Display', serif;
    background-color: white;
    color: #333;
    border: none;
    padding: 5px 10px;
    margin-left: 10px;
    cursor: pointer;
  }
  </style>