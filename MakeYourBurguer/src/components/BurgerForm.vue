<template>
  <div>
    <Message :msg="msg" v-show="msg" />
    <div id="div-form">
      <form id="burger-form" @submit="createBurger">
        <div class="input-container">
          <label for="nome">Nome do cliente:</label>
          <input
            type="text"
            id="nome"
            name="nome"
            v-model="nome"
            placeholder="Digite seu nome"
          />
        </div>
        <div class="input-container">
          <label for="pao">Tipo de pão:</label>
          <select name="pao" id="pao" v-model="pao">
            <option value="">Selecione o seu pão</option>
            <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">
              {{ pao.tipo }}
            </option>
          </select>
        </div>
        <div class="input-container">
          <label for="carne">Tipo de carne:</label>
          <select name="carne" id="carne" v-model="carne">
            <option value="">Selecione o tipo de carne</option>
            <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">
              {{ carne.tipo }}
            </option>
          </select>
        </div>
        <div id="opcionais-container" class="input-container">
          <label for="opcionais" id="opcionais-title"
            >Selecione os opcionais:</label
          >
          <div
            class="checkbox-container"
            v-for="opcional in opcionaisdata"
            :key="opcional.id"
          >
            <input
              type="checkbox"
              name="opcionais"
              v-model="opcionais"
              :value="opcional.tipo"
            />
            <span> {{ opcional.tipo }} </span>
          </div>
        </div>
        <div class="input-container">
          <input type="submit" class="submit-btn" value="Criar meu Burger!" />
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import Message from "./Message.vue";
export default {
  components: { Message },
  name: "BurgerForm",
  data() {
    return {
      paes: null,
      carnes: null,
      opcionaisdata: null,
      nome: null,
      pao: null,
      carne: null,
      opcionais: [],
      msg: null,
    };
  },
  methods: {
    async getIngredientes() {
      const req = await fetch("http://localhost:3000/ingredientes");
      const data = await req.json();

      this.paes = data.paes;
      this.carnes = data.carnes;
      this.opcionaisdata = data.opcionais;
    },
    async createBurger(e) {
      e.preventDefault();

      const data = {
        nome: this.nome,
        pao: this.pao,
        carne: this.carne,
        opcionais: Array.from(this.opcionais),
        status: "Solicitado",
      };
      const dataJson = JSON.stringify(data);

      const req = await fetch("http://localhost:3000/burgers", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: dataJson,
      });

      const res = await req.json();
      console.log("Resposta do servidor:", res);

      if (req.ok) {
        console.log("Hamburguer cadastrado");
      } else {
        console.log("Erro ao criar o pedido");
      }

      //Colocar uma msg de sistema
      this.msg = "Pedido realizado com sucesso!";

      setTimeout(() => (this.msg = ""), 3000);

      (this.nome = ""),
        (this.carne = ""),
        (this.pao = ""),
        (this.opcionais = "");
    },
  },
  mounted() {
    this.getIngredientes();
  },
};
</script>
<style scoped>
#burger-form {
  max-width: 400px;
  margin: 0 auto;
}
.input-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 15px;
}

label {
  font-weight: bold;
  margin-bottom: 15px;
  color: #222;
  padding: 5px 10px;
  border-left: 4px solid #fcba03;
}

input,
select {
  padding: 5px 10px;
  width: 300px;
}
#opcionais-container {
  flex-wrap: wrap;
  flex-direction: row;
}
#opcionais-title {
  width: 100%;
}

.checkbox-container {
  align-items: flex-start;
  display: flex;
  width: 50%;
  margin-bottom: 20px;
}
.submit-btn {
  border: 2px solid #222;
  color: #fcba03;
  background: #222;
  padding: 15px 0;
  font-weight: bold;
  font-size: 16px;
  margin: 0 auto;
  margin-right: 70px;
  transition: 0.5s;
  cursor: pointer;
}
.submit-btn:hover {
  color: #222;
  background: transparent;
}
.checkbox-container span,
.checkbox-container input {
  width: auto;
}
.checkbox-container span {
  font-weight: bold;
  margin-left: 6px;
}

#div-form {
  margin-left: 45px;
}
</style>
