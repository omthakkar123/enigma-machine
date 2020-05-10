<template>
  <div id="app">
    <input type="text" name="input" id="input" v-model="input" @keyup="enigma()" />
    <button @click="enigma()">Enigma</button>
    <button @click="rotate(r1)">Rotate</button>
    <!-- <h1>{{c3}}{{c2}}{{c1}}</h1> -->

    <!-- <p>{{JSON.stringify(r1)}}</p> -->
    <table>
      <tr v-for="(c,i) in r1" :key="i">
        <td>{{i}}-></td>
        <td>{{c}}</td>
        <td>{{r2[i]}}</td>
        <td>{{r3[i]}}</td>
      </tr>
    </table>

    <p>{{output}}</p>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      input: "A",
      output: "",
      c1: "A",
      c2: "A",
      c3: "A",
      r1: {
        A: "A",
        B: "B",
        C: "C",
        D: "D",
        E: "E",
        F: "F"
      },
      r2: {
        A: "A",
        B: "B",
        C: "C",
        D: "D",
        E: "E",
        F: "F"
      },
      r3: {
        A: "A",
        B: "B",
        C: "C",
        D: "D",
        E: "E",
        F: "F"
      }
    };
  },
  methods: {
    reflector(input) {
      for (var i = 0; i <= "F".charCodeAt() - "A".charCodeAt(); i++) {
        var inverse = "F".charCodeAt() - "A".charCodeAt() - i;
        inverse = inverse + "A".charCodeAt();
        var inew = i + "A".charCodeAt();
        if (input == String.fromCharCode(inew)) {
          console.log(String.fromCharCode(inew), String.fromCharCode(inverse));

          return String.fromCharCode(inverse);
        }
      }
    },
    rotor(o) {
      var temp = o["A"];
      for (var i = "A".charCodeAt(); i < "F".charCodeAt(); i++) {
        var c1ascii = i + 1;
        var inew = String.fromCharCode(c1ascii);
        o[String.fromCharCode(i)] = o[inew];
      }
      o["F"] = temp;
    },
    rotate() {
      if (this.c1 < "F") {
        var c1ascii = this.c1.charCodeAt() + 1;
        this.c1 = String.fromCharCode(c1ascii);
        this.rotor(this.r1);
      } else {
        this.c1 = "A";
        this.rotor(this.r1);
        if (this.c2 < "F") {
          var c2ascii = this.c2.charCodeAt() + 1;
          this.c2 = String.fromCharCode(c2ascii);
          this.rotor(this.r2);
        } else {
          this.c2 = "A";
          this.rotor(this.r2);
          if (this.c3 < "F") {
            var c3ascii = this.c3.charCodeAt() + 1;
            this.c3 = String.fromCharCode(c3ascii);
            this.rotor(this.r3);
          } else {
            this.c3 = "A";
            this.rotor(this.r3);
          }
        }
      }
      // console.log(this.c1, this.c2);
    },
    enigma() {
      // this.output = this.r1[this.r2[this.r3[this.reflector(this.r3[this.r2[this.r1[this.input]]])]]];
      // this.output = this.reflector(this.r3[this.r2[this.r1[this.input]]]);
      // this.output = this.r2[this.r1[this.input]];
      this.output = this.r1[this.reflector(this.r1[this.input])];
      this.rotate();
      // console.log(this.rotor1(this.input))
    }
  }
};
</script>
<style>
* {
  font-family: "Fira Code", Courier, monospace;
  word-wrap: break-word;
}
input {
  width: 70vw;
}
</style>