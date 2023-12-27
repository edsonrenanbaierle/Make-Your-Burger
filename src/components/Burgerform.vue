<template>
  <div>
    <p>mensagem</p>
    <div id="main-container">
      <form id="burger-form">
        <div class="input-container">
          <label for="name">Nome do cliente:</label>
          <input type="text" id="name" name="name" v-model="name" placeholder="Digite o seu nome">
        </div>
        <div class="input-container">
          <label for="bread">Escolha o pão:</label>
          <select name="bread" id="bread" v-model="bread">
            <option value="">Selecione o seu pão</option>
            <option value="integral">Integral</option>
          </select>
        </div>
        <div class="input-container">
          <label for="meat">Escolha a carne do seu Burger:</label>
          <select name="meat" id="meat" v-model="bread">
            <option value="">Selecione o tipo de carne</option>
            <option value="picanha">Picanha</option>
          </select>
        </div>
        <div class="input-container" id="optional-container">
          <label id="optional-title" for="optional">Escolha os opcionais:</label>
          <div class="checkbox-container">
            <input type="checkbox" v-model="optional" name="optional" value="Salame">
            <span>Salame</span>
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
export default {
  name: 'Burgerform'
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