<template>
    <div class="calculator">
        <div class="display">{{ disp || "0" }}</div> 
        <div @click="clear" class="btn">AC</div>
        <div @click="sign" class="btn">+/-</div>
        <div @click="percent" class="btn">%</div>
        <div @click="divide" class="btn operator">/</div>
        <div @click="append('7')" class="btn">7</div>
        <div @click="append('8')" class="btn">8</div>
        <div @click="append('9')" class="btn">9</div>
        <div @click="mult" class="btn operator">*</div>
        <div @click="append('4')" class="btn">4</div>
        <div @click="append('5')" class="btn">5</div>
        <div @click="append('6')" class="btn">6</div>
        <div @click="sub" class="btn operator">-</div>
        <div @click="append('1')" class="btn">1</div>
        <div @click="append('2')" class="btn">2</div>
        <div @click="append('3')" class="btn">3</div>
        <div @click="add" class="btn operator">+</div>
        <div @click="append('0')" class="btn zero">0</div>
        <div @click="dot" class="btn">.</div>
        <div @click="eval" class="btn operator">=</div>
    </div>
</template>
<script lang="ts">
export default {
    data() {
        return {
            disp: '',
            previous: null,
            operator: null,
            operator_clicked: false
        }
    },
    methods: {
        clear() {
            this.disp = '';
        },
        sign() {
            this.disp = this.disp.charAt(0) === '-' ? this.disp.slice(1) : '-' + this.disp;
        },
        percent() {
            this.disp = (parseFloat(this.disp)/100).toString();
        },
        append(num: string) {
            if (this.operator_clicked) {
                this.disp='';
                this.operator_clicked = false;
            }
            this.disp = this.disp.concat(num);
        },
        dot() {
            // only add dot if it was not just typed
            if (this.disp.indexOf('.') === -1) {
                this.append('.');
            } 
        },
        divide() {
            this.operator = (a:number, b:number) => a/b;
            this.previous = this.disp;
            this.operator_clicked = true;
        },
        mult() {
            this.operator = (a:number, b:number) => a*b;
            this.previous = this.disp;
            this.operator_clicked = true;
        },
        sub () {
            this.operator = (a:number, b:number) => a-b;
            this.previous = this.disp;
            this.operator_clicked = true;
        },
        add () {
            this.operator = (a:number, b:number) => a+b;
            this.previous = this.disp;
            this.operator_clicked = true;
        },
        eval () {
            this.disp = (this.operator(parseFloat(this.previous), parseFloat(this.disp))).toString();
        }
    }
}

</script>
<style scoped>
    .calculator {
        font-size: 40px;
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        grid-auto-rows: minmax(50px, auto);
    }
    .display {
        grid-column: 1 / 5;
        background-color: red;
        border-radius: 8px;
    }
    .zero {
        background-color: #1a1a1a;
        grid-column: 1 / 3;
    }
    
    .btn {
        background-color: #1a1a1a;
        border-radius: 8px;
        border: 1px solid darkgray;
        margin: 5px;
    }
    .btn:hover {
        background-color: #3a3a3a;
    }
    .operator {
        background-color: darkslategrey;
        color: white;
    }
</style>