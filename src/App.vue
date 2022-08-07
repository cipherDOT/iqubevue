<script>
import { initializeApp } from 'firebase/app'
import { getFirestore, setDoc, doc } from 'firebase/firestore/lite'

const config_vars = {
    "apiKey": "AIzaSyAgPotrNQzZcM22I6a5Ic_v-fp1DDSUwRA",
    "authDomain": "iqubedj.firebaseapp.com",
    "projectId": "iqubedj",
    "storageBucket": "iqubedj.appspot.com",
    "messagingSenderId": "635827728558",
    "appId": "1:635827728558:web:c2af1752d667eb61a4fd3f",
    "measurementId": "G-HQ300JWPHP",
    "databaseURL" : "https://iqubedj-default-rtdb.firebaseio.com/",
}

let firebaseApp = initializeApp(config_vars);
let db = getFirestore(firebaseApp)


export default {
	name: "home",
	data() {
		return {
			user_data: {
				fullname: '',
				username: '',
				email: '',
				password1: '',
				password2: '',
				mobile: '',
				country: '',
			}
		}
	},
	methods: {
		add() {
			if (this.user_data.password1 == this.user_data.password2) {
				setDoc(doc(db, "data", "hBxRvymVDtyBPt0hhuQn"), this.user_data)
                Object.keys(this.user_data).forEach(x => {
                    this.user_data[x] = ''
                })
                alert("Successfull");
			} else {
				alert("Passwords don't match");
			}
		}
	}
}

</script>

<template>
<div id="homeform">
	<form @submit.prevent="add" class="formfield">
        <div class="field">
            <label for="">Fullname:</label>
            <input type="text" name="fullname" required="required" v-model="user_data.fullname">
        </div>
        <div class="field">
            <label for="">Username:</label> 
            <input type="text" name="username" required="required" v-model="user_data.username">
        </div>
        <div class="field">
            <label for="">Email:</label>
            <input type="text" name="email" required="required" v-model="user_data.email">
        </div>
        <div class="field">
            <label for="">Password:</label>
            <input type="password" name="password1" required="required" v-model="user_data.password1">
        </div>
        <div class="field">
            <label for="">Confirm password:</label>
            <input type="password" name="password2" required="required" v-model="user_data.password2">
        </div>
        <div class="field">
            <label for="">Mobile:</label>
            <input type="text" name="mobile" required="required" v-model="user_data.mobile">
        </div>
        <div class="field">
            <label for="">Country:</label>
            <input type="text" name="country" required="required" v-model="user_data.country">
        </div>
		<input type="submit" class="btn">
	</form>
</div>
</template>

<style scoped>
@import './assets/main.css';

#homeform {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
}

.formfield {
    display: flex;
    flex-direction: column;
    gap: 20px;
}

.field {
    display: flex;
    justify-content: space-between;
    gap: 5px;
}

.field > input {
    border: none;
    outline: none;
    border-bottom: 2px solid var(--secondary);
}

.btn {
    background: var(--secondary);
    border-radius: 50vh;
    outline: none;
    border: none;
}

@media only screen and (max-width: 700px) {
	.formfield {
		width: 80%;
	}
}
</style>
