<template>
    <div class="calculator">
        <div class="display">{{ current || '0' }}</div>
        <div class="btns" @click="clear">C</div>
        <div class="btns" @click="sign">+/-</div>
        <div class="btns" @click="percent">%</div>
        <div class="btns operators" @click="divide">/</div>
        <div @click="append('7')" class="btns">7</div>
        <div @click="append('8')" class="btns">8</div>
        <div @click="append('9')" class="btns">9</div>
        <div class="btns operators" @click="times">x</div>
        <div @click="append('4')" class="btns">4</div>
        <div @click="append('5')" class="btns">5</div>
        <div @click="append('6')" class="btns">6</div>
        <div class="btns operators" @click="minus">-</div>
        <div @click="append('1')" class="btns">1</div>
        <div @click="append('2')" class="btns">2</div>
        <div @click="append('3')" class="btns">3</div>
        <div class="btns operators" @click="sum">+</div>
        <div @click="append('0')" class=" btns zero">0</div>
        <div @click="dot" class="btns ">.</div>
        <div class="btns operators" @click="equal">=</div>
      
    </div>
</template>

<script>
export default {
    data(){
        return{
            previous: null,
            current: '',
            operation: null,
            operatorClicked:false,
        }
    },
    methods: {
        clear(){
            this.current = '';
        },
        sign(){
            if (this.current != '') {                
                this.current = this.current.charAt(0) ===  '-'?
                this.current.slice(1) : `-${this.current}`;
            }
        },
        percent(){
            this.current = `${parseFloat(this.current) / 100}`;  
        },
        append(number){
            if (this.operatorClicked) {
                this.current='';
                this.operatorClicked=false;
            }
            this.current = `${this.current}${number}`;
        },
        dot(){
            if (this.current.indexOf('.') === -1 ) {
                this.append('.');
            }
        },
        setPrevious(){
            this.previous = this.current;
            this.operatorClicked = true;            
        },
        divide(){
            this.operation = (a, b) => a/b; 
            this.setPrevious();
        },
        times(){
            this.operation = (a, b) => a*b;
            this.setPrevious();
        },
        minus(){
            this.operation = (a, b) => b-a;
            this.setPrevious();
        },
        sum(){
            this.operation = (a, b) => a+b;            
            this.setPrevious();
        },
        equal(){
            this.current = `${this.operation(
                parseFloat(this.current),
                parseFloat(this.previous)
            )}`;

            this.previous=null;            
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    
    
    .calculator div{
        text-align: center;
    }
    .calculator{
        margin: 0 auto;
        width: 300px;
        font-size: 40px;
        display: grid; 
        grid-template-columns: repeat(4, 1fr);
        grid-auto-rows: minmax(50px, auto);
        font-family: monospace;     
        
    }

    .display{
        grid-column: 1 / 5;
        background-color: darkslategray;
        color: white;
    }

    .zero{
        grid-column:  1 / 3;
    }

    .btns{
        background-color: #eee;
        border: 1px solid darkslategray;
        cursor: pointer;
    }

    .operators{
        background-color: orange;
        color: white;
    }

</style>
