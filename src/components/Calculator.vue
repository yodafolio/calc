<template>
  <v-container>
    <v-row>
      <v-container>
        <v-col v-if="this.calc" class="display"
          >total : {{ total }} <span></span
        ></v-col>
        <v-col v-else class="display">rgNum : {{ rgNum }} <span></span></v-col>
      </v-container>
    </v-row>
    <v-row>
      <v-container class="number">
        <v-row>
          <v-col v-for="n in numbers" :key="n" cols="3"
            ><v-btn block depressed @click="createNumber(n)">{{
              n
            }}</v-btn></v-col
          >
        </v-row>
      </v-container>
      <v-container class="operators">
        <v-row>
          <v-col v-for="c in operators" :key="c"
            ><v-btn
              block
              depressed
              color="lime accent-3"
              @click="getOperator(c)"
              >{{ c }}</v-btn
            ></v-col
          >
        </v-row>
      </v-container>
    </v-row>
    <v-row>
      <v-container>
        <v-col>{{ total }}</v-col>
        <v-col>{{ operator }}</v-col>
      </v-container>
    </v-row>
  </v-container>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

@Component
export default class Calculator extends Vue {
  private total = 0;
  private rgNum = 0;
  private arrNum: number[] = [];
  private operator = '';
  private calc = false;
  private numbers: number[] = [1, 2, 3, 4, 5, 6, 7, 8, 9, 0];
  private operators: string[] = ['C', '+', '-', '*', '/', '%', '='];

  public resetData(): void {
    this.total = 0;
    this.rgNum = 0;
    this.arrNum = [];
    this.operator = '';
    this.calc = false;
  }

  private calcFnc(arr: number[], operator: string) {
    let calc;
    if (operator === '+') calc = (a: number, b: number) => b + a;
    if (operator === '-') calc = (a: number, b: number) => b - a;
    if (operator === '*') calc = (a: number, b: number) => a * b;
    if (operator === '/') calc = (a: number, b: number) => a / b;

    const reduce = (f: any, acc: any, iter?: any) => {
      if (!iter) {
        iter = acc[Symbol.iterator]();
        acc = iter.next().value;
      }
      for (const a of iter) acc = f(a, acc);
      return acc;
    };
    const res = reduce(calc, arr);
    return res;
  }

  private conditionBoolean = (operator: string): boolean => {
    const res =
      operator === '+' ||
      operator === '-' ||
      operator === '/' ||
      operator === '*' ||
      operator === '%';
    return res;
  };

  public createNumber(num: number): void {
    if (this.conditionBoolean(this.operator)) this.calc = false;
    const a = this.rgNum.toString();
    const b = num.toString();
    this.rgNum = Number(a + b);
  }

  private setCalc(operator: string) {
    if (!this.total) this.total = this.rgNum;
    if (this.rgNum > 0) this.arrNum.push(this.rgNum);
    if (this.arrNum.length < 2 && this.conditionBoolean(operator))
      this.operator = operator;
    this.rgNum = 0;
    this.calc = true;
    if (this.arrNum.length === 2) {
      this.total = this.calcFnc(this.arrNum, this.operator);
      this.arrNum = [];
      this.arrNum.push(this.total);
      this.conditionBoolean(operator)
        ? (this.operator = operator)
        : (this.operator = '');
    }
  }

  public getOperator(operator: string): void {
    if (operator === 'C') return this.resetData();
    if (this.conditionBoolean(operator)) {
      this.setCalc(operator);
    } else if (operator === '=') {
      this.setCalc(operator);
    }
  }
  // private get sumTotal() {
  //   return false;
  // }
}
</script>
