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
        <div class="flex justify-center items-center min-h-screen select-none bg-[#ecf0f3]">
            <div class="p-5 rounded-lg shadow-[13px_13px_20px_#cbced1,-13px_-13px_20px_#ffffff] w-full max-w-sm sm:max-w-md md:max-w-lg">
                <div class="mb-2 w-full h-18 text-4xl outline-none border-0 text-right pr-2 bg-[#ecf0f3] rounded-lg shadow-inner shadow-[#cbced1] shadow-[inset_-8px_-8px_8px_#ffffff]">
                    <input type="text" v-model="screen" @keydown.enter="evalExpression" placeholder="0" class="w-full outline-none bg-transparent" />
                </div>

                <div class="grid grid-cols-4 gap-2">
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 shadow-[5px_5px_8px_#00000020,-5px_-5px_8px_#ffff] bg-pink-600 text-white hover:shadow-[inset_5px_5px_8px_#e60073,_inset_-5px_-5px_8px_#ff3399]" @click="backspace">CE</button>
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 hover:bg-white" @click="calculate('factorial')">x!</button>
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 hover:bg-white" @click="appendToScreen('(')">(</button>
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 hover:bg-white" @click="appendToScreen(')')">)</button>
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 bg-[#33cc33] text-white" @click="clearScreen">AC</button>
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 hover:bg-white" @click="calculate('tan')">tan</button>
                </div>

                <div class="grid grid-cols-4 gap-2">
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 hover:bg-white" @click="calculate('sin')">sin</button>
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 hover:bg-white" @click="appendToScreen('9')">9</button>
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 hover:bg-white" @click="appendToScreen('8')">8</button>
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 hover:bg-white" @click="calculate('pi')">π</button>
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 hover:bg-white" @click="appendToScreen('cos')">cos</button>
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 hover:bg-white" @click="appendToScreen('7')">7</button>
                </div>
                
                <div class="grid grid-cols-4 gap-2">
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 hover:bg-white" @click="calculate('/')">/</button>
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 hover:bg-white" @click="appendToScreen('4')">4</button>
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 hover:bg-white" @click="appendToScreen('5')">5</button>
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 hover:bg-white" @click="appendToScreen('6')">6</button>
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 hover:bg-white" @click="appendToScreen('%')">%</button>
                </div>
                
                <div class="grid grid-cols-4 gap-2">
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 hover:bg-white" @click="appendToScreen('*')">*</button>
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 hover:bg-white" @click="appendToScreen('1')">1</button>
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 hover:bg-white" @click="appendToScreen('2')">2</button>
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 hover:bg-white" @click="appendToScreen('3')">3</button>
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 hover:bg-white" @click="appendToScreen('-')">-</button>
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 hover:bg-white" @click="calculate('sqrt')">√</button>
                </div>

                <div class="grid grid-cols-4 gap-2">
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 hover:bg-white" @click="appendToScreen('+')">+</button>
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 hover:bg-white" @click="calculate('pow')">x<sup>y</sup></button>
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 hover:bg-white" @click="appendToScreen('0')">0</button>
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 hover:bg-white" @click="appendToScreen('.')">.</button>
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 bg-[#33ccff] text-white" @click="evalExpression">=</button>
                    <button class="btn w-full h-[40px] text-[16px] border-none outline-none rounded transition duration-100 hover:bg-white" @click="calculate('e')">e</button>
                </div>
            </div>
        </div>
    </div>
</template>