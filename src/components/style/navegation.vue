<template>
	<div>
		<div v-if="this.user.authenticated">
			 <md-button>{{ this.user.name}}</md-button>
			 <router-link tag="md-button" v-bind:to="{ name: 'changePassword' }" class="md-raised">Cambiar Contraseña</router-link>
			 <md-button class="md-raised" v-on:click="logout">Cerrar sesion</md-button>
		</div>

		<div v-else>
			<router-link tag="md-button" to="login" class="md-raised">Iniciar Sesión</router-link>
			<router-link tag="md-button" v-bind:to="{ name:'registerUser' }" class="md-raised">Registro</router-link>

		</div>

	</div>
</template>

<script type="text/javascript">
	import { auth } from './../../utils/auth.js'

	export default {
		data() {
			return {
				user: auth.getUserInformation(this)
			}
		},
		methods: {
			setUser() {
				this.user = auth.getUserInformation(this);
			},
			logout(){
				auth.logout(this,'login');
			}
		},
		watch: {
			$route() {
				this.setUser();
			}
		}
	}
</script>
