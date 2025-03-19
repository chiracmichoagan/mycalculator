<script setup lang="ts">
import { onBeforeUnmount, onMounted, ref } from 'vue';
const screen = ref('');
const appendToScreen = (char: string) => {
    screen.value += char;
}
const backspace = () => {
    screen.value = screen.value.slice(0, -1);
};
const clearScreen = () => {
    screen.value = '';
};
const calculate = (func: string) => {
    let result = '';
    try {
        switch (func) {
            case 'sin':
                result = Math.sin(parseFloat(screen.value)).toString();
                break;

            case 'cos':
                result = Math.cos(parseFloat(screen.value)).toString();
                break;
            case 'tan':
                result = Math.tan(parseFloat(screen.value)).toString();
                break;
            case 'sqrt':
                result = Math.sqrt(parseFloat(screen.value)).toString();
                break;
            case 'log':
                result = Math.log(parseFloat(screen.value)).toString();
                break;
            case 'pi':
                result = Math.PI.toString();
                break;
            case 'e':
                result = Math.E.toString();
                break;
            case 'factorial':
                result = factorial(parseInt(screen.value)).toString();
                break;
            case 'pow':
                result = Math.pow(parseFloat(screen.value), 2).toString();
                break;
            default:
                result = "Invalide operation";
                break;
        }
    } catch (error) {
        result = 'ERROR'
    }
    screen.value = result;
}

const factorial = (num: number) => {
    let result = 1;
    for (let i = 1; i <= num; i++) {
        result *= i;
    }
    return result;
}
const evalExpression = () => {
    try {
        screen.value = eval(screen.value).toString();
    } catch (error) {
        screen.value = 'Error';
    }
};

const handleKeypress = (event: KeyboardEvent) => {
    if (event.key === 'Enter') {
        evalExpression();
    }
};
onMounted(() => {
    document.addEventListener('keydown', handleKeypress);
});

onBeforeUnmount(() => {
    document.removeEventListener('keydown', handleKeypress);
});
</script>

<template>
    <div>
        <div class="p-0 m-0 flex justify-center items-center min-h-screen select-none bg-[#ecf0f3]">
            <div class="ml-7 p-5 rounded-lg shadow-[13px_13px_20px_#cbced1,-13px_-13px_20px_#ffffff]">
                <div
                    class="mb-2 w-auto h-18 text-4xl outline-none border-0 text-right pr-2 bg-[#ecf0f3] rounded-lg shadow-inner shadow-[#cbced1] shadow-[inset_-8px_-8px_8px_#ffffff]">
                    <input type="text" v-model="screen" @keydown.enter="evalExpression" name="" id="" placeholder="0">
                </div>
                <div class="btns">
                    <div class="row">
                        <button
                            class="w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  bg-pink-600 text-white hover:shadow-[inset_5px_5px_8px_#e60073,_inset_-5px_-5px_8px_#ff3399]"
                            @click="backspace">CE</button>
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white"
                            @click="calculate('factorial')">x!</button>
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white"
                            @click="appendToScreen('(')">(</button>
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white"
                            @click="appendToScreen(')')">)</button>
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white"
                            @click="appendToScreen('%')">%</button>
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100  bg-[#33cc33] text-white hover:shadow-[inset_5px_5px_8px_#2eb82e,_inset_-5px_-5px_8px_#33cc33]"
                            @click="clearScreen">AC</button>

                    </div>
                </div>
                <div class="btns">
                    <div class="row">
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white"
                            @click="calculate('sin')">sin</button>
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white">7</button>
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white">8</button>
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white"
                            @click="calculate('pi')">π</button>
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white"
                            @click="appendToScreen('9')">9</button>
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white"
                            @click="appendToScreen('/')">/</button>

                    </div>
                </div>
                <div class="btns">
                    <div class="row">
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white"
                            @click="calculate('cos')">cos</button>
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white"
                            @click="calculate('log')">log</button>
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white"
                            @click="appendToScreen('4')">4</button>
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white"
                            @click="appendToScreen('5')">5</button>
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white"
                            @click="appendToScreen('6')">6</button>
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white"
                            @click="appendToScreen('*')">*</button>

                    </div>
                </div>
                <div class="btns">
                    <div class="row">
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white"
                            @click="calculate('tan')">tan</button>
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white"
                            @click="calculate('sqrt')">√</button>
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white"
                            @click="appendToScreen('1')">1</button>
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white"
                            @click="appendToScreen('2')">2</button>
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white"
                            @click="appendToScreen('3')">3</button>
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white"
                            @click="appendToScreen('-')">-</button>
                    </div>
                </div>
                <div class="btns">
                    <div class="row">
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white"
                            @click="calculate('e')">e</button>
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white"
                            @click="calculate('pow')">x
                            <sup>y</sup></button>
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white"
                            @click="appendToScreen('0')">0</button>
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white"
                            @click="appendToScreen('.')">.</button>
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  bg-[#33ccff] text-white shadow-inner shadow-[#66d9ff] hover:shadow-inner hover:shadow-[#00ace6]"
                            @click="evalExpression">=</button>
                        <button
                            class="btn w-[60px] h-[30px] text-[16px] border-none outline-none m-[5px] rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff]  hover:shadow-[inset_5px_5px_8px_rgba(16,16,16,0.1),inset_-5px_-5px_8px_#fff] hover:bg-white"
                            @click="appendToScreen('+')">+</button>
                    </div>
                </div>
            </div>
        </div>

    </div>

</template>
