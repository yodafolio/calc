<template>
  <div class="container">
    <div class="section1">
      <div class="display">0</div>
    </div>
    <div class="section2">
      <div class="number">
        <div class="number-btn">1</div>
        <div class="number-btn">2</div>
        <div class="number-btn">3</div>
        <div class="number-btn">4</div>
        <div class="number-btn">5</div>
        <div class="number-btn">6</div>
        <div class="number-btn">7</div>
        <div class="number-btn">8</div>
        <div class="number-btn">9</div>
        <div class="number-btn">0</div>
      </div>
      <div class="calc">
        <div class="calc-btn">+</div>
        <div class="calc-btn">-</div>
        <div class="calc-btn">%</div>
        <div class="calc-btn">/</div>
      </div>
    </div>
  </div>
</template>

<script>
import { Vue } from 'vue-property-decorator';

export default class Calculator extends Vue {}
</script>

<style lang="scss">
.container {
  border: 1px solid rebeccapurple;
  .section1 {
    padding: 12px;
    font-size: 2em;
    font-weight: bold;
    background-color: rgba($color: #000000, $alpha: 0.5);
  }
  .section2 {
    display: flex;
    justify-content: space-between;
    background-color: rgba($color: #af2323, $alpha: 0.5);
    .number {
      display: flex;
      text-align: center;
      flex-wrap: wrap;
      width: 80%;
      .number-btn {
        width: 33.3333%;
        padding: 10px 0;
        border: 1px solid rgb(212, 212, 212);
        box-sizing: border-box;
      }
    }
    .calc {
      width: 20%;
      text-align: center;
      .calc-btn {
        padding: 10px 0;
        width: 100%;
        color: blanchedalmond;
        background-color: darkolivegreen;
        border: 1px solid rgb(212, 212, 212);
        box-sizing: border-box;
      }
    }
  }
}
</style>
