<template>
  <div class="login">
    <div>
      <form @submit.prevent="submit"> 
        <div>
          <label for="email">Email:</label>
          <!-- <div class="email"> -->
          <input class="email" type="text" name="email" v-model="form.email" />
          <!-- </div> -->
        </div>
        <div>
          <label for="password">Password:</label>
          <input type="password" name="password" v-model="form.password" />
        </div>
        <div class="botao">
          <button type="submit">Entrar</button>
        </div>
      </form>
      <p v-if="showError" id="error">Email ou Password estão incorrectos</p>
    </div>
  </div>
</template>

<script>
import { mapActions } from "vuex";

export default {
  name: "Login",
  components: {},
  data() {
    return {
      form: {
        email: "",
        password: "",
      },
      showError: false
    };
  },

  methods: {
    ...mapActions(["LogIn"]),
    async submit() {
      const User = new FormData();
      User.append("email", this.form.email);
      User.append("password", this.form.password);

      console.log(this.form.email)
      console.log(this.form.password)
      

      try {
          await this.LogIn(User);
          console.log("teste")
          this.$router.push("/posts");
          this.showError = false
      } catch (error) {
        this.showError = true
      }
    },
  },
};
</script>

<style scoped>
* {
  box-sizing: border-box;
}
 
label {
  padding: 12px 12px 12px 0;
  display: inline-block;
}

button[type="submit"] {
  background-color: #f0833b ;
  color: white;
  margin-top: 30px;
  padding: 8px 30px;
  cursor: pointer;
  border-radius: 30px;  
}

.botao {
  padding-left: 150px;
}

.email {
   margin-left: 35px; 
} 

input {
  margin: 5px;
 /*  margin-left: 60px; */
  box-shadow: 0 0 15px 4px rgba(0, 0, 0, 0.06);
  padding: 10px;
  border-radius: 30px;
  
}
#error {
  color: red;
}

</style>
