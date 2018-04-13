<template>
<div id="signUp">
	<button class="input__btnSignUp"
		@click="signUp=false"
		v-if="signUp">
		Close
	</button>
	<button class="input__btnSignUp"
		@click="signUp=true"
		v-else	
	>
		Sign Up
	</button>
	<section class="comments__signUp" v-show="signUp">
		<form class="singUp__form">
			<label class="form__label">
				Name
				<input type="text" placeholder="Name" v-model="dateNewUser.name">
			</label>
			<label class="form__label">
				E-mail
				<input type="email" placeholder="e-mail" v-model="dateNewUser.email">
			</label>
			<label class="form__label">
				Picture
				<div class="select" 
					v-bind:style="styleObject"
					@click="changeState()"
				>
					<div class="select__option" 
						v-if="dateNewUser.picProfile">
						<img class="option__img"
							:src="dateNewUser.picProfile" 
						>
					</div>
					<div class="select__option" 
						v-for="picture in pictures"
						v-else
					>
						<img class="option__img"
							:src="picture" 
							@click="dateNewUser.picProfile=picture"
						>
					</div>
				</div>
			</label>
			<button
				class="input__btnSignUp input__btnSignUp--send"
				@click="insertUser()"
			>
				Send
			</button>
		</form>
	</section>
</div>
</template>
<script>
import ft02 from '../assets/ft-perfil-02.png'
import ft03 from '../assets/ft-perfil-03.png'
import ft04 from '../assets/ft-perfil-04.png'
import ft05 from '../assets/ft-perfil-05.png'
import ft06 from '../assets/ft-perfil-06.png'
import ft07 from '../assets/ft-perfil-07.png'
import ft08 from '../assets/ft-perfil-08.png'
import ft09 from '../assets/ft-perfil-09.png'
import ft10 from '../assets/ft-perfil-10.png'
import ft11 from '../assets/ft-perfil-11.png'
import ft12 from '../assets/ft-perfil-12.png'
import ft13 from '../assets/ft-perfil-13.png'
import ft14 from '../assets/ft-perfil-14.png'

export default{
	name: 'UserList',
	props:{
		// dateNewUser:{type:Object},
		// post:{type:Boolean},
		// pictures:{type:Array}
	},
	data(){
		return{
			signUp:false,
			post:false,
			styleObject:{
				overflowY:'hidden',
				height: '30px',
				padding: '0',
				borderRadius: '0',
			},
			dateNewUser:{
				name:'',
				email:'',
				picProfile:''
			},
			pictures:[
				ft02, ft03, ft04, ft05, ft06, ft07 , ft08, ft09, ft10, ft11, ft12, ft13, ft14
			],
			users:[
				{
					name:'Rômulo Tunala',
					picProfile: ft02,
					email:'romulotunala@gmail.com'
				},
				{
					name:'Dalianny Vieira',
					picProfile: ft04,
					email:'daliannyvieira@gmail.com'
				},
				{
					name:'Aline Froes',
					picProfile: ft11,
					email:'alinefroes@gmail.com'
				}
			]
		}
	},
	created(){
		this.$emit('users', this.users)
	},
	methods:{
		changeState(){
			if(this.styleObject.overflowY == 'hidden'){
				this.styleObject.overflowY = 'scroll'	
				this.styleObject.height = '100px'
				this.styleObject.padding = '3px'
				this.styleObject.borderRadius = '5px'
				if(this.dateNewUser.picProfile != '' || this.dateNewUser.picProfile != null){
					this.dateNewUser.picProfile = ''
				}
			}else{
				this.styleObject.overflowY = 'hidden'
				this.styleObject.height = '30px'
				this.styleObject.padding = '0'
				this.styleObject.borderRadius = '0'
			}			
		},
		insertUser(){
			if(this.dateNewUser.email == '' || this.dateNewUser.name == ''){
				alert('Please, enter all the values.')
			}else if(this.dateNewUser.picProfile == ''){
				alert('Please, choose an avatar.')
			}else{
				this.users.push(this.dateNewUser)
				this.$emit('dateNewUser', this.dateNewUser = {
					name:'',
					email:'',
					picProfile:''
				})
				this.signUp=false
			}
			
		}
	}
}
</script>
<style scoped>
.signUp{
	
}
.input__btnSignUp{
	padding: 5px;
	margin:10px;
	border-radius: 3px;
	border:none;
	background:#E30059;
	color:#FFF;
}
.input__btnSignUp--send{
	width: 20%;
	position: absolute;
	bottom: 10px;
	right: 10px;

}
.comments__signUp{
	width: 100%;
	min-height: 18vh;
	position: absolute;
	z-index: 2;
	top:50px;
	left:0;
	display: flex;
	justify-content: center;
	align-items: flex-start;

	background-color: #3DB5B0;

}
.singUp__form{
	width: 85%;
	margin: 20px 0;
	display: flex;
	flex-direction: column;
}
.form__label{
	margin:5px;
	display: flex;
	justify-content: space-between;
}
.form__label input{
	padding: 5px;
}
.select{
	width: 45px;
	/*height: 30px;*/
	margin-right: auto;
	margin-left: 12%;
	background-color: #3DB5B0;
	/*overflow: hidden;*/
	position: relative;	
}
.select::after {
  content:"▼";
  font-size:0.5em;
  font-family:arial;
  position:absolute;
  top:50%;
  right:5px;
  transform:translate(0, -50%);
}
.select:hover::after {
  content:"";
}
.select:hover{
	width: 40px;
	/*height: 100px;*/
	/*padding: 3px;*/
	/*border-radius: 5px;*/
	position: relative;
	z-index: 99;
  	/*overflow-y: scroll;*/
}
.select:hover::-webkit-scrollbar {
	width: 4px;
	border-radius: 5px;
    background: yellow;
}
.select:hover::-webkit-scrollbar-thumb {
    border-radius: 5px;
    background: red; 
}
.select__option{
	border:none;
	background-color:;
}
.option__img{ 
	width: 30px;
 }
</style>