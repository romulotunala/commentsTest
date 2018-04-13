<template>
<div class="comments">
	<section class="comments__input">
		<select class="input__selectUser" v-model="user">
			<option disabled value="">Change User</option>
			<option v-for="user in users" :value="user.name">
				{{ user.name }}
			</option>
		</select>
		<UsersList class="UsersList"
			@pictures="value =>{pictures = value}"
			@users="value => {users = value}"
			@dateNewUser="value =>{dateNewUser = value}"
		>
			<!-- :dateNewUser="dateNewUser" -->
			<!-- :pictures="pictures" -->
			<!-- :post="post" -->
		</UsersList>
		<textarea 
			class="input__textarea"
			v-model="textComment" 
			placeholder="Escreva seu comentário">
		</textarea>
		<button class="input__btSend" @click="sendComment()">Send</button>
	</section>
	
	<section class="comments__commentsUsers">
		<div class="commentsUsers__items" v-for="comment in comments">
			<img class="commentsUsers__picture" :src="comment.picProfile">
			<h2 class="comments__name">{{ comment.name }}</h2>
			<p class="comments__text">{{ comment.textComment }}</p>
			<hr>
		</div>
	</section>
</div>
</template>
<script>
import UsersList from './UsersList.vue'
import ft02 from '../assets/ft-perfil-02.png'
import ft04 from '../assets/ft-perfil-04.png'

export default{
	name: 'Comments',
	data(){
		return{
			user:'',
			users:'',
			pictures:'',
			dateNewUser:{
				name:'',
				email:'',
				picProfile:''
			},
			textComment:'',
			// pictures:[
			// 	{pic:'ft02'}, 
			// 	{pic:'ft05'},
			// 	{pic:'ft04'},
			// 	{pic:'ft03'},
			// 	{pic:'ft06'},
			// 	{pic:'ft07'},
			// 	{pic:'ft08'},
			// 	{pic:'ft09'},
			// 	{pic:'ft10'},
			// 	{pic:'ft11'},
			// 	{pic:'ft12'},
			// 	{pic:'ft13'},
			// 	{pic:'ft14'}
			// ],
			comments:[
				{
					name:'Rômulo Tunala',
					picProfile:ft02,
					email:'romulotunala@gmail.com',
					textComment:'Li Europan lingues es membres del sam familie. Lor separat existentie es un myth. Por scientie, musica, sport etc., li tot Europa usa li sam vocabularium. Li lingues differe solmen in li grammatica, li pronunciation e li plu commun vocabules...'
				},
				{
					name:'Aline Froes',
					picProfile:ft04,
					email:'alinefroes@gmail.com',
					textComment:'Li Europan lingues es membres del sam familie. Lor separat existentie es un myth. Por scientie, musica, sport etc., li tot Europa usa li sam vocabularium. Li lingues differe solmen in li grammatica, li pronunciation e li plu commun vocabules. Omnicos directe al desirabilit? de un nov lingua franca: on refusa continuar payar custosi traductores. It solmen va esser necessi far uniform grammatica, pronunciation e plu sommun paroles.'
				}
			]		
		}
	},
	computed:{
		userSelected(){
			let user = this.users.filter(user => user.name === this.user)

			if(user){
				return user
			}

			return null
		}
	},
	methods:{
		selecPicProfile(){
			
		},
		sendComment(){
			this.comments.unshift({
				name: this.userSelected[0].name,
				email: this.userSelected[0].email,
				picProfile: this.userSelected[0].picProfile,
				textComment: this.textComment
			})
			this.textComment = ''
		}
	},
	components:{
		UsersList
	}
}
</script>
<style scoped>
.comments{
	max-width: 320px;
	max-height: 60vh;
	min-height: 600px;
	margin: 0 auto;
	box-shadow: 0 0 10px #333;

	/*position: absolute;
	bottom:0;
	right: 0;*/
}
.comments__input{
	width: 100%;
	height: 150px;
	background: #85CFE8;
	position: relative;
	display: flex;
	flex-direction: row;
	flex-wrap: wrap;
	justify-content: space-between;
	align-items: flex-start;
	align-content: space-between;
}
.input__selectUser:focus,
.input__textarea:focus{
	outline: none;
	box-shadow: 0 0 3px inset;
}
.input__selectUser{
	height: 35px;
	padding: 0 7px;
	background: none;
	border: none;
}
.input__selectUser option{
	background: #85CFE8;
	padding: 0;
}
.input__textarea{
	width: 100%;
	height: 105px;
	padding: 12px;
	border: none;
	background:transparent;
	resize: none
}
.input__btSend{
	width: 40px;
	height: 40px;
	border:none;
	border-radius: 50%;
	background-color: #3DB5B0bb;
	position: absolute;
	bottom: 10px;
	right: 10px;
	color: #FFF;
}
.input__btSend:active{
	background-color: #3DB5B0;
}
.comments__commentsUsers{
	width: 100%;
	max-height: 40vh;
	min-height: 450px;
	background: #E30059;
	overflow: auto;
}
.commentsUsers__items{
	min-height: 20vh;
	padding: 10px;
	padding-bottom: 20px;
	margin:10px 5px;
	border-radius: 30px;
	border-bottom-right-radius: 0;
	border-bottom: 1px solid #E30059;
	background-color: #F6A800;
	display: flex;
	flex-wrap: wrap;
	align-items: center;
	align-content: flex-start;
}
.commentsUsers__items:last-child{
	border:none;
}
.commentsUsers__picture{
	width: 10%;
	margin: 5px;
}
.comments__name{
	color: #FFF;
}
.comments__text{
	width: 95%;
	margin: 0 auto;
	color: #FFF;
}
</style>