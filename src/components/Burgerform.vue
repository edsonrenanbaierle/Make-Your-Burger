<template>
  <div>
    <Message :msg="msg" v-show="msg"/>
    <div id="main-container">
      <form id="burger-form" @submit="createBurger">
        <div class="input-container">
          <label for="name">Nome do cliente:</label>
          <input type="text" id="name" name="name" v-model="name" placeholder="Digite o seu nome">
        </div>
        <div class="input-container">
          <label for="bread">Escolha o pão:</label>
          <select name="bread" id="bread" v-model="bread">
            <option value="">Selecione o seu pão</option>
            <option v-for="pao in breadsServer" :key="pao.id" :value="pao.tipo">{{pao.tipo}}</option>
          </select>
        </div>
        <div class="input-container">
          <label for="meat">Escolha a carne do seu Burger:</label>
          <select name="meat" id="meat" v-model="meat">
            <option value="">Selecione o tipo de carne</option>
            <option v-for="carne in meatsServer" :key="carne.id" :value="carne.tipo">{{ carne.tipo }}</option>
          </select>
        </div>
        <div class="input-container" id="optional-container">
          <label id="optional-title" for="optional">Escolha os opcionais:</label>
          <div class="checkbox-container" v-for="opcionais in optionalDataServer" :key="opcionais.id">
            <input type="checkbox" v-model="optional" name="optional" :value="opcionais.tipo">
            <span>{{opcionais.tipo}}</span>
          </div>
        </div>
        <div class="input-container">
          <input type="submit" class="submit-btn" value="Criar meu Burger!">
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import Message from './Message.vue';
export default {
  name: 'Burgerform',
  data(){
    return {
      breadsServer: null, 
      meatsServer: null,
      optionalDataServer: null,
      name: null,
      bread: null,
      meat: null,
      optional: [],
      msg: null
    }
  },
  methods: {
    async getIngredientes() {
      const req = await fetch("http://localhost:3000/ingredientes");
      const data = await req.json();

      this.breadsServer = data.paes;
      this.meatsServer = data.carnes;
      this.optionalDataServer = data.opcionais;
    },
    async createBurger(e) {

      e.preventDefault()

      const data = {
        nome: this.name,
        carne: this.meat,
        pao: this.bread,
        opcionais: Array.from(this.optional),
        status: 'Solicitado'
      }

      const dataJson = JSON.stringify(data)

      const req = await fetch("http://localhost:3000/burgers", {
        method: "POST",
        headers: {"Content-Type": "application/json"},
        body: dataJson
      })

      const res = await req.json()

      //msg
      this.msg = `Pedido ${res.id} realizado com sucesso!`

      setTimeout(() => {
        this.msg = ''
      }, 3000);

      // limpar dados
      this.name = ''
      this.meat = ''
      this.bread = ''
      this.optional = []

    }
  },
  mounted(){
    this.getIngredientes();
  }, 
  components: {
    Message
  }
}
</script>


<style scoped>
  #main-container {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  #burger-form {
    max-width: 400px;
  }

  .input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
  }

  label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;
    padding: 5px 10px;
    border-left: 4px solid #FCBA03;
  }

  input, select {
    padding: 5px 10px;
    width: 300px;
  }

  #optional-container {
    flex-direction: row;
    flex-wrap: wrap;
  }
  
  #optional-title {
    width: 100%;
  }

  .checkbox-container{
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
  }

  .checkbox-container span, .checkbox-container input{
    width: auto;
  }

  .checkbox-container span {
    margin-left: 6px;
    font-weight: bold;
  }

  .submit-btn {
    background-color: #222;
    color: #FCBA03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    cursor: pointer;
    transition: .5s;
  }

  .submit-btn:hover {
    background-color: transparent;
    color: #222;
  }
</style>