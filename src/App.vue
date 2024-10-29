<template>
	<div id="App" class="grid-container">
 <div class="userA" v-for="(usuario, i) in usuarios.slice(0, 1)" :key="i">
		<img :src="usuario.picture.large" class="user-img"/> 
		<h3>{{ usuario.name.first }} {{ usuario.name.last }}</h3> 
		<input type="color" v-model="usuario.colorFondo" /><br>
		<input type="text" v-model="usuario.chatInput" /><br>
		<button @click="agregarChat(i)">Enviar</button>
	</div>
  
	<chatComponent :messages="messages" :usuarios="usuarios" /> 
  
	<div class="userB" v-for="(usuario, i) in usuarios.slice(1)" :key="i">
		<img :src="usuario.picture.large" class="user-img"/> 
		<h3>{{ usuario.name.first }} {{ usuario.name.last }}</h3> 
		<input type="color" v-model="usuario.colorFondo" /><br>
		<input type="text" v-model="usuario.chatInput" /><br>
		<button @click="agregarChat(i + 1)">Enviar</button>
	</div>
  
	</div>
  </template>
  
  <script>
  import chatComponent from "./components/chatComponent.vue";
  import axios from "axios";
  
  export default {
	name: "App",
	components: {
	chatComponent,
	},
	data() {
	return {
		usuarios: [],
		messages: [],
	};
	},
	async mounted() {
	const url = "https://randomuser.me/api?results=2";
	const { data } = await axios.get(url);
	this.usuarios = data.results.map((usuario) => ({
		...usuario,
		chatInput: "",
		colorFondo: "#ffffff", // color de fondo inicial
	}));
	},
	methods: {
	agregarChat(index) {
		const chatInput = this.usuarios[index].chatInput.trim();
		if (chatInput !== "") {
		this.messages.push({
			user: index,
			text: chatInput,
			colorFondo: this.usuarios[index].colorFondo, // agregar el color de fondo al mensaje
		});
		this.usuarios[index].chatInput = "";
		}
	},
	},
  };
  </script>
  
  <style>
  .grid-container {
	display: grid;
	grid-template-columns: repeat(3, 1fr);
	grid-gap: 10px;
  }
  
  .userA, .userB {
	display: flex;
	flex-direction: column;
	justify-content: center;
  }
  
  .user-img {
	width: 200px;
  }
  
  </style> 