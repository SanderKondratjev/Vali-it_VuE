<template>
  <div class="home">
    <h1>Logi sisse</h1>
    <input v-model="username" placeholder="Kasutajatunnus">
    <input v-model="password" placeholder="Parool">
    <button v-on:click="login()">Logi sisse</button>
    <br>
    <br>{{login2}}
    <h1>Logi välja</h1>
    <button v-on:click="logout()">Logi välja</button>
    <br>
    <br>{{logout2}}
    <h1>Kontode nimekiri</h1>
    <table class="center" border="1">
      <tr>
        <th>Nimi</th>
        <th>Konto nr</th>
        <th>Saldo</th>
        <th>E-mail</th>
        <th>Lukus?</th>
      </tr>
      <tr v-for="customers in accounts">
        <td>{{ customers.name }}</td>
        <td>{{ customers.accountNr }}</td>
        <td>{{ customers.balance }}</td>
        <td>{{ customers.email }}</td>
        <td>{{ customers.locked }}</td>
      </tr>
    </table>
    <h2>Ava konto</h2>
    <input v-model="accountNr1" placeholder="Uus konto number">
    <input v-model="name1" placeholder="Ees- ja perekonnanimi">
    <input v-model="email1" placeholder="E-mail">
    <button v-on:click="createAcc()">Ava konto</button>
    <br>
    <br>{{avatud}}
    <h2>Vaata konto seisu</h2>
    <input v-model="accountNr" placeholder="Sisesta oma konto number">
    <button v-on:click="saldo()">Saldoseis</button>
    <br>
    <br>{{balance}}
    <h2>Lae raha</h2>
    <input v-model="accountNr2" placeholder="Sisesta konto number">
    <input v-model="balance2" placeholder="Sisesta summa, mida soovid kanda">
    <button v-on:click="deposit()">Lae raha</button>
    <br>
    <br>{{laetud}}
    <h2>Võta raha</h2>
    <input v-model="accountNr3" placeholder="Sisesta konto number">
    <input v-model="balance3" placeholder="Sisesta summa, mida soovid võtta">
    <button v-on:click="withdraw()">Võta raha</button>
    <br>
    <br>{{voetud}}
    <h2>Kontode vaheline kanne</h2>
    <input v-model="accountNr4" placeholder="Konto nr, kust soovid raha kanda">
    <input v-model="accountNr5" placeholder="Konto nr, kuhu soovid raha kanda">
    <input v-model="balance4" placeholder="Sisesta summa, mida soovid võtta">
    <button v-on:click="transfer()">Kanna</button>
    <br>
    <br>{{kantud}}
  </div>
</template>

<script>

export default {
  data: function () {
    return{
      'balance':'',
      'accountNr':'',
      'name1':'',
      'accountNr1':'',
      'email1':'',
      'avatud':'',
      'accountNr2':'',
      'balance2':'',
      'laetud':'',
      'accountNr3':'',
      'balance3':'',
      'voetud':'',
      'accountNr4':'',
      'accountNr5':'',
      'balance4':'',
      'kantud':'',
      accounts: [],
      'username':'',
      'password':''
    }
  },
  methods:{
    'saldo':function (){
      this.$http.get('http://localhost:8080/banksql/2/' + this.accountNr)
          .then(response => {
            this.balance = response.data
          });
    },
    'createAcc':function (){
      this.$http.post('http://localhost:8080/banksql/1', {
        accountNr: this.accountNr1,
        name: this.name1,
        email: this.email1
      })
          .then(response => {
            this.avatud = "Super, konto on avatud"
          });
    },
    'deposit':function (){
      this.$http.put('http://localhost:8080/banksql/3/' + this.accountNr2, {
        balance: this.balance2,
      })
          .then(response => {
            this.laetud = "Kontole " + this.accountNr2 +
                " on laetud " + this.balance2 + " €."
          });
    },
    'withdraw':function (){
      this.$http.put('http://localhost:8080/banksql/4/' + this.accountNr3, {
        balance: this.balance3,
      })
          .then(response => {
            this.voetud = "Kontolt " + this.accountNr3 +
                " on võetud " + this.balance3 + " €."
          });
    },
    'transfer':function (){
      this.$http.put('http://localhost:8080/banksql/5/' +
          this.accountNr4 + "/" + this.accountNr5, {
        balance: this.balance4,
      })
          .then(response => {
            this.kantud = "Kontolt " + this.accountNr4 +
                " on võetud " + this.balance4 + " € ning kantud kontole " +
                this.accountNr5
          });
    },
    'login':function (){
      this.$http.post('http://localhost:8080/banksql/login',{
        username: this.username,
        password: this.password,})
          .then((response) => {
            localStorage.setItem('user-token', response.data)
            this.$http.defaults.headers.common['Authorization'] = "Bearer " + response.data
            this.login2 = "Sisse logitud"
          });
    },
    'logout': function () {
      localStorage.removeItem('user-token')
      location.reload()
      this.logout2 = "Välja logitud"
    }
  },
  mounted() {
    this.$http.get("http://localhost:8080/banksql/8")
        .then(response => this.accounts = response.data);
  }
}
</script>
