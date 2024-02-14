<script setup>
import { computed, ref } from 'vue'
import BasicInput from './components/BasicInput.vue';



// return fetch('/api/users/token', {
//         method: 'POST',
//         headers: {
//             'Content-Type': 'application/json'
//         },
//         body: JSON.stringify({
//             login: thisLogin,
//             email: thisEmail,
//             password: md5(thisPassword)
//         })
//     })
//     .then(response => response.json())
//     .then(data => {
//         console.log(data)
//         return data
//     })
//     .catch(error => console.error(error))
// }

const onBlur = (event) => {
  console.log(event.target.value)
}

const onFocus = (event) => {
  console.log(event.target.value)
}

const loginValid = (event) => {
  console.log(event.target.value)
  if (!isValidLogin(event.target.value)) {
    errorMessageLogin.value = 'Login is not valid'
    console.log('Login is not valid')
  }
  else {
    errorMessageLogin.value = ''
    validMessageLogin.value = 'Login is valid'
    console.log('Login is valid')
  }
}

function isValidLogin(login) {
  return /^[a-zA-Z0-9]{3,}$/.test(login);
}


const emailValid = (event) => {
  console.log(event.target.value);
  if (!isValidEmail(event.target.value)) {
    messageEmail.value = 'Email is not valid';

    console.log('Email is not valid');
  } else {
    email.value = event.target.value;
    messageEmail.value = ''; // Efface le message si l'email est valide
    // messageEmail.style.color = ''; // Réinitialise la couleur du texte
    console.log('Email is valid');
  }
};

function isValidEmail(email) {
  return /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/.test(email);
}

const passwordValid = (event) => {
  console.log(event.target.value)
  if (!isValidPassword(event.target.value)) {
    messagePassword.value = 'Password does not contain at least 8 characters, a capital letter, a lowercase letter and a number.'
    errorMessage.value = 'Password does not contain at least 8 characters, a capital letter, a lowercase letter and a number.'
    console.log('Password is not valid')
  }
  else {
    password.value = event.target.value
    messagePassword.value = ''
    errorMessage.value = ''
    console.log('Password is valid')
  }
}

function isValidPassword(password) {
  // renvoit true si le mot de passe contient au moins 8 caractères, une majuscule, une minuscule et un chiffre
  return /^(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).{8,}$/.test(password);
}

function passwordConfValid(event) {
  console.log(event.target.value)
  if (!isValidPasswordConf(event.target.value)) {
    messagePasswordConf.value = 'Password confirmation does not match the password'
    errorMessage.value = 'Password confirmation does not match the password'
    console.log('Password confirmation does not match the password')
  }
  else {
    passwordConf.value = event.target.value
    messagePasswordConf.value = ''
    errorMessage.value = ''
    console.log('Password confirmation match the password')
  }
}

function isValidPasswordConf(passwordConf) {
  // renvoit true si le mot de passe contient au moins 8 caractères, une majuscule, une minuscule et un chiffre
  return passwordConf === document.getElementById('password').value
}

const errorMessageLogin = ref('')
const validMessageLogin = ref('')

const messageEmail = ref('')
const messagePassword = ref('')
const messagePasswordConf = ref('')
const errorMessage = ref('aa')
const email = ref('')
const errorSubmit = ref('')
const login = ref('')
const password = ref('')
const passwordConf = ref('')





const disabled = computed(() => {
  return errorMessage.value !== '' || email.value === '' || login.value === '' || password.value === '' || passwordConf.value === '' ? true : false
})

</script>

<template>
  <h1>Mon Application</h1>

  <form action="/login" method="post">
    <fieldset>
      <legend>Connexion</legend>

      <BasicInput 
      id="Login" 
      label="Login" 
      type="text" 
      placeholder="Laruiss" 
      :errorMessage="errorMessageLogin"
      :validMessage="validMessageLogin" 
      :modelValue="login" 
      @input:modelValue="loginValid($event)" 
      />

      <BasicInput
      id="email"
      label="Email"
      type="email"
      placeholder="stanislas.ormieres@yahoo.com"
      :errorMessage="messageEmail"
      :validMessage="messageEmail"
      :modelValue="email"
      @input:modelValue="emailValid($event)"
      />

      <BasicInput
      id="password"
      label="Password"
      type="password"
      placeholder="Azerty.123"
      :errorMessage="messagePassword"
      :validMessage="messagePassword"
      :modelValue="password"
      @input:modelValue="passwordValid($event)"
      />

      <BasicInput
      id="confipassword"
      label="Confirmation password"
      type="password"
      placeholder="Azerty.123"
      :errorMessage="messagePasswordConf"
      :validMessage="messagePasswordConf"
      :modelValue="passwordConf"
      @input:modelValue="passwordConfValid($event)"
      />


        <!-- <div>
          <label for="Login">Login</label>
          <input type="text" id="Login" name="Login" placeholder="Enter the login" @blur="loginValid($event)">
          <p :class="messageClass">
            {{ messageLogin }}
          </p>
        </div>
        <div>
          <label for="email">Email</label>
          <input type="email" id="email" name="email" placeholder="Enter the email" @blur="emailValid($event)">
          <p>
            {{ messageEmail }}
          </p>
        </div>
        <div>
          <label for="password">Password</label>
          <input type="password" id="password" name="password" placeholder="Enter the password"
            @blur="passwordValid($event)">
          <p :class="messageClass">
            {{ messagePassword }}
          </p>
        </div>
        <div>
          <label for="confipassword">Confirmation password</label>
          <input type="password" id="confipassword" name="confipassword" placeholder="Enter the password"
            @blur="passwordConfValid($event)">
          <p :class="messageClass">
            {{ messagePasswordConf }}
          </p>
        </div> -->
      <!-- 
      <div>
        <label for="login">Login</label>
        <input name="login" type="login" id="login">
        <p class="message"></p>
      </div>
      <div>
        <label for="email">email</label>
        <input name="email" type="email" v-model="email" id="email" @focus="onFocus($event)" @blur="onBlur($event)">
        <p>
          {{ email }}
        </p>
        <p class="message"></p>
      </div>
      <div>
        <label for="password">Password</label>
        <input name="password" type="password" id="password">

        <p class="message"></p>
      </div>
      <div>
        <label for="password">Confirmation Password</label>
        <input name="password" type="password" id="password">
        <p class="message"></p>
      </div> -->
      <p>
        <button type="submit" :disabled="disabled"><b>Se Connecter</b></button>
      </p>
    </fieldset>
  </form>
</template>

<style scoped>
.valid {
  color: red;
}

/* .invalid{
  color: green;
} */</style>