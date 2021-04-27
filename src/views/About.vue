<template>
  <div class="about">
    <h1>Lesson 1</h1>
    <h5>Min</h5>
    <input v-model.number="minA">
    <input v-model.number="minB">
    <button v-on:click="min()">Min</button>
      {{minAnswer}}
    <h5>Max</h5>
    <input v-model.number="maxA">
    <input v-model.number="maxB">
    <button v-on:click="max()">Max</button>
    {{maxAnswer}}
    <h5>Abs</h5>
    <input v-model.number="abs">
    <button v-on:click="absMidagi()">Abs</button>
    {{absAnswer}}
    <h5>Is Even</h5>
    <input v-model.number="even">
    <button v-on:click="isEven()">Is Even</button>
    {{evenAnswer}}
    <h5>Min3</h5>
    <input v-model.number="min3a">
    <input v-model.number="min3b">
    <input v-model.number="min3c">
    <button v-on:click="min3()">Min3</button>
    {{min3Answer}}
    <h5>Max3</h5>
    <input v-model.number="max3a">
    <input v-model.number="max3b">
    <input v-model.number="max3c">
    <button v-on:click="max3()">Max3</button>
    {{max3Answer}}
    <h5>Korrutustabel</h5>
    <input v-model.number="x"/>
    <input v-model.number="y"/>
    <button v-on:click="tabel">Korrutustabel</button>
    <table border="1">
      <tr v-for="row in table">
        <td v-for="column in row">{{column}}</td>
      </tr>
    </table>
  </div>
</template>

<script>
function min() {
  if (this.minA < this.minB) {
    this.minAnswer = this.minA;
  } else {
    this.minAnswer = this.minB;
  }
}
function max() {
  if (this.maxA > this.maxB) {
    this.maxAnswer = this.maxA;
  } else {
    this.maxAnswer = this.maxB;
  }
}
function abs() {
  if (this.abs > 0) {
    this.absAnswer = this.abs;
  } else {
    this.absAnswer = this.abs * -1;
  }
}
function even() {
  if (this.even % 2 == 0) {
    this.evenAnswer = "True";
  } else {
    this.evenAnswer = "False";
  }
}
function min3() {
  if (this.min3a <= this.min3b && this.min3a <= this.min3c) {
    this.min3Answer = this.min3a;
  } else if (this.min3b <= this.min3c && this.min3b <= this.min3a){
    this.min3Answer = this.min3b;
  } else {
    this.min3Answer = this.min3c;
  }
}
function max3() {
  if (this.max3a >= this.max3b && this.max3a >= this.max3c) {
    this.max3Answer = this.max3a;
  } else if (this.max3b >= this.max3c && this.max3b >= this.max3a){
    this.max3Answer = this.max3b;
  } else {
    this.max3Answer = this.max3c;
  }
}
export default {
  data: function () {
    return {
      'minA': 0,
      'minB': 0,
      'minAnswer': 0,
      'maxA':0,
      'maxB':0,
      'maxAnswer':0,
      'abs': 0,
      'absAnswer': 0,
      'even': 0,
      'evenAnswer': 0,
      'min3a': 0,
      'min3b': 0,
      'min3c': 0,
      'min3Answer': 0,
      'max3a': 0,
      'max3b': 0,
      'max3c': 0,
      'max3Answer': 0,
      "x":0,
      "y":0,
      "table":[[]]
    }
  },
  methods: {
    'min':min,
    'max':max,
    'absMidagi':abs,
    'isEven':even,
    'min3':min3,
    'max3':max3,
    'tabel':function (){
      for (let i = 1; i <= this.x; i++) {
        this.table[i-1] = []
        for (let j = 1; j <= this.y; j++) {
          this.table[i-1][j-1]=i*j;
        }
      }
      this.table.splice()
    }
  }
}
</script>