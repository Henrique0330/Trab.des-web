<script setup>
import { ref } from 'vue'

const usuario = ref({
  nome: 'Matheus',
  sobrenome: 'Henrique',
  email: 'matheus&Henrique@gmail.com',
  cidade: '',
  estado: '',
  cep: '',
  avatar: '',
  hobbies: {
    esporte: false,
    leitura: false,
    viagens: false,
    musica: false
  },
  linguagemPreferida: ''
});


const hobbies = ref({
  esporte: false,
  leitura: false,
  viagens: false,
  musica: false
})

const mostrarPerfil = ref(false)

function handleFileUpload(e) {
  const target = e.target
  console.log(target)
  console.log("awdoaiwdhuaiowdhawdiou")
  if (target && target.files) {
    const file = target.files[0]
    usuario.value.avatar = URL.createObjectURL(file)
  }
}

function salvarPerfil() {
  mostrarPerfil.value = true



}
function voltar() {
  mostrarPerfil.value = false
}

const estados = [
  { uf: 'AC', name: 'Acre' },
  { uf: 'AL', name: 'Alagoas' },
  { uf: 'AP', name: 'Amapá' },
  { uf: 'AM', name: 'Amazonas' },
  { uf: 'BA', name: 'Bahia' },
  { uf: 'CE', name: 'Ceará' },
  { uf: 'DF', name: 'Distrito Federal' },
  { uf: 'ES', name: 'Espírito Santo' },
  { uf: 'GO', name: 'Goiás' },
  { uf: 'MA', name: 'Maranhão' },
  { uf: 'MT', name: 'Mato Grosso' },
  { uf: 'MS', name: 'Mato Grosso do Sul' },
  { uf: 'MG', name: 'Minas Gerais' },
  { uf: 'PA', name: 'Pará' },
  { uf: 'PB', name: 'Paraíba' },
  { uf: 'PR', name: 'Paraná' },
  { uf: 'PE', name: 'Pernambuco' },
  { uf: 'PI', name: 'Piauí' },
  { uf: 'RJ', name: 'Rio de Janeiro' },
  { uf: 'RN', name: 'Rio Grande do Norte' },
  { uf: 'RS', name: 'Rio Grande do Sul' },
  { uf: 'RO', name: 'Rondônia' },
  { uf: 'RR', name: 'Roraima' },
  { uf: 'SC', name: 'Santa Catarina' },
  { uf: 'SP', name: 'São Paulo' },
  { uf: 'SE', name: 'Sergipe' },
  { uf: 'TO', name: 'Tocantins' }
]

</script>

<template>

  <body>
    <form v-if="!mostrarPerfil">
      <div>
        <label for="txtnome">Nome:</label>
        <br>
        <input type="text" name="" v-model="usuario.nome" id="txtnome">
      </div>
      <br>
      <div>
        <label for="txtsobrenome">Sobrenome:</label>
        <br>
        <input type="text" v-model="usuario.sobrenome" id="txtsobrenome">
      </div>
      <br>
      <div>
        <label for="txtemail">Email:</label>
        <br>
        <input type="email" v-model="usuario.email" id="txtemail">
      </div>
      <br>
      <div>
        <label for="txtcidade">Cidade:</label>
        <br>
        <input type="text" v-model="usuario.cidade" id="txtcidade">
      </div>
      <br>
      <div>
        <label for="txtestado">Estado:</label>
        <br>
        <select v-model="usuario.estado" name="txtestado" id="txtestado">
          <option v-for="estado in estados" value="{{ estado.uf }}">{{ estado.name }}</option>

        </select>
      </div>
      <br>
      <div>
        <label for="cep">CEP:</label>
        <br>
        <input v-model="usuario.cep" type="number" id="cep">
      </div>
      <br>
      <div>
        <label for="avatar">Avatar:</label>
        <input v-on:change="handleFileUpload" type="file" accept="image/*" id="avatar">
        <br>
        <img style="height: 250px;" :src="usuario.avatar">
      </div>
      <br>
      <div>

        <label for="hoob">Hoobies:</label>
        <br>
        <input v-model="usuario.hobbies.esporte" type="checkbox" id="esporte">
        <label for="esporte">Esportes</label>

        <input v-model="usuario.hobbies.musica" type="checkbox" id="musica">
        <label for="musica">Música</label>

        <input v-model="usuario.hobbies.viagens" type="checkbox" id="viagens">
        <label for="viagens">Viagens</label>

        <input v-model="usuario.hobbies.leitura" type="checkbox" id="leitura">
        <label for="leitura">Leitura</label>

        <br>
        <br>
      </div>
      <div>
        <label for="linguagem">linguagem:</label>
        <input v-model="usuario.linguagemFavorita" type="text" id="linguagem">
      </div>


      <div>
        <button type="button" @click="salvarPerfil">enviar</button>
      </div>
    </form>

    <div v-if="mostrarPerfil">
      <h1>Perfil de {{ usuario.nome }}</h1>
      <img style="height: 250px;" :src="usuario.avatar">
      <p>Nome: {{ usuario.nome }}</p>
      <p>Sobrenome: {{ usuario.sobrenome }}</p>
      <p>Email: {{ usuario.email }}</p>
      <p>Cidade: {{ usuario.cidade }}</p>
      <p>Estado: {{ usuario.estado }}</p>
      <p>CEP: {{ usuario.cep }}</p>
      <p>Hobbies:
        <span v-if="usuario.hobbies.esporte">Esportes </span>
        <span v-if="usuario.hobbies.musica">Música </span>
        <span v-if="usuario.hobbies.viagens">Viagens </span>
        <span v-if="usuario.hobbies.leitura">Leitura </span>
      </p>
      <p>Linguagem Preferida: {{ usuario.linguagemFavorita }}</p>
      <button @click="voltar">Voltar</button>
    </div>


  </body>

</template>

<style scoped>
.avatar {
  width: 200px;
  height: 200px;
  border-radius: 50%;
}

.form-enter-active,
.form-leave-active {
  transition: opacity 0.5s ease;
}

.form-enter-from,
.form-leave-to {
  opacity: 0;
}
</style>
