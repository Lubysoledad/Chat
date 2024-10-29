<template>
	<div class="chat-container">
		<div v-for="(message, index) in messages" :key="index" class="chat-message" :style="{ 'justify-content': message.user === 0 ? 'flex-start' : 'flex-end', 'background-color': usuarios[message.user].colorFondo }">
			<strong>
				{{ usuarios[message.user].name.first }}
				{{ usuarios[message.user].name.last }}:</strong>
			{{ message.text }}
		</div>
	</div>
</template>

<script>
export default {
	name: "chatComponent",
	props: {
		messages: {
			type: Array,
			required: true,
		},
		usuarios: {
			type: Array,
			required: true,
		},
	},
};
</script>

<style scoped>
.chat-container {
	border: 1px solid #ccc;
	padding: 10px;
	margin-top: 20px;
	display: flex;
	flex-direction: column;
}
.chat-message {
	margin-bottom: 10px;
	padding: 10px;
	border-radius: 5px;
	color: white; /* Cambia esto al color que prefieras para el texto */
}
</style>
