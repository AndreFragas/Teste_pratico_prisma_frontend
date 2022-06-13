<template>
    <div class="container">
      <h1>Gerador de Planilha</h1>
      <hr />
      <div class="form-todo form-group">
          <h3>E-mail</h3>
          <p>
          <input placeholder="Insira seu e-mail" type="text" name="author" class="form-control" v-model="email" />
          </p>
          <h3>Estado</h3>
          <select class="form-select form-select-lg mb-3" aria-label=".form-select-lg example" v-model="estado">
              <option selected></option>
              <option value="RO">Rondônia</option>
              <option value="AC">Acre</option>
              <option value="AM">Amazonas</option>
              <option value="RR">Roraima</option>
              <option value="PA">Pará</option>
              <option value="AP">Amapá</option>
              <option value="TO">Tocantins</option>
              <option value="MA">Maranhão</option>
              <option value="PI">Piauí</option>
              <option value="CE">Ceará</option>
              <option value="RN">Rio Grande do Norte</option>
              <option value="PB">Paraíba</option>
              <option value="PE">Pernambuco</option>
              <option value="AL">Alagoas</option>
              <option value="SE">Sergipe</option>
              <option value="BA">Bahia</option>
              <option value="MG">Minas Gerais</option>
              <option value="ES">Espírito Santo</option>
              <option value="RJ">Rio de Janeiro</option>
              <option value="SP">São Paulo</option>
              <option value="PR">Paraná</option>
              <option value="SC">Santa Catarina</option>
              <option value="RS">Rio Grande do Sul</option>
              <option value="MT">Mato Grosso do Sul</option>
              <option value="GO">Goiás</option>
              <option value="DF">Distrito Federal</option>
          </select>
          <br>
          <div id="buttomAlert">
              <button v-on:click="chamarAPI" type="submit" class="btn btn-primary">Gerar Planilha</button>
          </div>
      </div>
      <hr/>
    </div>

</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  methods: {
    chamarAPI(){
      if (this.estado.trim() === '' && this.email.trim() === ''){
        //alert("Todos os campos estão em branco!");
        return "Todos os campos estão em branco!";
      } else if(this.estado.trim() === ''){
        //alert("O campo de estado está em branco!");
        return "Estado não foi selecionado!";
      } else if (this.email.trim() === ''){
        //alert("O campo de e-mail está em branco!");
        return "O campo de e-mail está em branco!";
      }
      var raw = JSON.stringify(this.estado);
      var raw2 = JSON.stringify(this.email);

      var myHeaders = new Headers();
      myHeaders.append("Content-Type", "application/json");

      var requestOptions = {
        method: 'Post',
        body: raw, raw2,
        headers: myHeaders,
        redirect: 'follow'
      };

      fetch("https://localhost:7036/api/projeto", requestOptions)
        .then(response => response.text())
        .then(result => console.log(result))
        .catch(error => console.log('error', error));
      
      this.estado = "";
      this.email = "";
    }
  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
