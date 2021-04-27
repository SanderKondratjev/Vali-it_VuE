<template>
  <div class="home">
    <input v-model="email" placeholder="Enter your e-mail"/>
    <button v-on:click="register()">Register</button>
    <table border="1">
      <tr v-for="email in emails">
        <td>{{email}}</td>
      </tr>
    </table>
  </div>
</template>

<script>

export default {
  name: 'Home',
  data: function () {
    return{
      'email': '',
      'emails':["esimene@mail.ee", "teine@mail.ee", "jne@mail.ee"]
    }
  },
  methods:{
    'register':function (){
      this.emails.push(this.email);
    }
  }
}
</script>
