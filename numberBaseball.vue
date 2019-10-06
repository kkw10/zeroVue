<template>
    <div>
        <h1>{{ result }}</h1>
        <form @submit.prevent="onSubmitForm">
            <input ref="answer" v-model="inputValue" maxlength="4" minlength="4">
            <button type="submit">입력</button>
        </form>
        <div>
            시도: {{ tries.length }}
        </div>
        <ul>
            <li v-for="t in tries">
                <div>{{ t.try }}</div>
                <div>{{ t.result }}</div>
            </li>
        </ul>
    </div>
</template>

<script>
    const getNumbers = () => {
        const candidates = [1,2,3,4,5,6,7,8,9];
        const array = [];
        for(let i = 0; i < 4; i += 1) {
            const chosen = candidates.splice(Math.floor(Math.random() * (9 - i)), 1)[0];
            array.push(chosen);
        }

        return array;
    }

    export default{
        data() {
            return {
                answer: getNumbers(),
                tries: [],
                inputValue: '',
                result: '',
            }
        },

        methods: {
            onSubmitForm(e) {
                if(this.inputValue === this.answer.join('')) {
                    this.tries.push({
                        try: this.inputValue,
                        result: '홈런'
                    });

                    this.result = '홈런';
                    this.answer = getNumbers();
                    this.tries = [];
                    alert('게임을 다시 시작합니다.');

                } else {
                    if(this.tries.length >= 9) {
                        this.result = `10번을 넘게 틀려서 실패했습니다. 정답은 ${this.answer.join(',')} 입니다.`;
                        
                        alert('게임을 다시 시작합니다.');

                        this.answer = getNumbers();
                        this.tries = [];
                    }

                    let strike = 0;
                    let ball = 0;

                    const answerArray = this.inputValue.split('').map(v => parseInt(v));

                    for(let i = 0; i < answerArray.length; i += 1) {
                        if(answerArray[i] === this.answer[i]) {
                            strike++;

                        } else if(this.answer.includes(answerArray[i])) {
                            ball++;

                        }
                    }

                    this.tries.push({
                        try: this.inputValue,
                        result: `${strike} 스트라이크, ${ball} 볼입니다.`
                    })                    
                }

                this.inputValue = '';
                this.$refs.answer.focus();
            }
        }
    }
</script>

<style>

</style>