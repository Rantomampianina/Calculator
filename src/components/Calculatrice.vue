<template>
  <body>
    <div class="calculator">
    <div class="affiche">{{ courrent || '0'}}</div>
    <div @click="efface" class="btn">C</div>
    <div @click="signe" class="btn">+/-</div>
    <div @click="pourcentage" class="btn">%</div>
    <div @click="division" class="btn operation">:</div>
    <div @click="ajouter('7')" class="btn">7</div>
    <div @click="ajouter('8')" class="btn">8</div>
    <div @click="ajouter('9')" class="btn">9</div>
    <div @click="croix" class="btn operation">x</div>
    <div @click="ajouter('4')" class="btn">4</div>
    <div @click="ajouter('5')" class="btn">5</div>
    <div @click="ajouter('6')" class="btn">6</div>
    <div @click="moins" class="btn operation">-</div>
    <div @click="ajouter('1')" class="btn">1</div>
    <div @click="ajouter('2')" class="btn">2</div>
    <div @click="ajouter('3')" class="btn">3</div>
    <div @click="plus" class="btn operation">+</div>
    <div @click="ajouter('0')" class="btn zero">0</div>
    <div @click="point" class="btn">.</div>
    <div @click="egal" class="btn operation">=</div>
  </div>
  </body>
</template>

<script>
export default {
  data() {
    return {
      precedent: null,
      courrent: '',
      operation: null,
      operationClique: false,
    }
  },
  methods: {
    efface() {
      this.courrent = '';
    },
    signe() {
      this.courrent = this.courrent.charAt(0) === '-' ?
        this.courrent.slice(1) : `-${this.courrent}`;
    },
    pourcentage() {
      this.courrent = `${parseFloat(this.courrent) / 1000}`
    },
    ajouter(nombre) {
      if (this.operationClique) {
        this.courrent = '';
        this.operationClique = false;
      }
      this.courrent = `${this.courrent}${nombre}`;
    },
    point() {
      if (this.courrent.indexOf('.') === -1) {
        this.ajouter('.');
      }
    },
    setPrecedent() {
      this.precedent = this.courrent;
      this.operationClique = true;
    },
    division() {
      this.operation = (a, b) => a / b;
      this.setPrecedent();
    },
    croix() {
      this.operation = (a, b) => a * b;
      this.setPrecedent();
    },
    moins() {
      this.operation = (a, b) => a - b;
      this.setPrecedent();
    },
    plus() {
      this.operation = (a, b) => a + b;
      this.setPrecedent();
    },
    egal() {
      this.courrent = `${this.operation(parseFloat(this.courrent), parseFloat(this.precedent))}`;
      this.precedent = null;
    }
  },
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>

<style scoped>

.calculator {
  margin: 0 auto;
  width: 400px;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}

.affiche {
  text-align: center;
  grid-column: 1 / 5;
  background-color: #333;
  color: white;
}

.zero {
  grid-column: 1 / 3;
}

.btn {
  text-align: center;
  align-items: center;
  background-color: #eee5e5;
  border: 1px solid #999;
}

.btn:hover {
  cursor: pointer;
}

.operation {
  color: white;
  background-color: orange;
}
</style>
