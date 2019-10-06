<template>
    <div>
        <h1>{{ result }}</h1>
        <form v-on:submit="onSubmitForm">
            <input ref="answer" v-model="inputValue" maxlength="4">
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
    export default{
        data() {
            return {
                tries: [],
                inputValue: '',
                result: '',
            }
        },

        methods: {
            onSubmitForm(e) {
                e.preventDefault();
                this.tries.push({
                    try: this.inputValue,
                    result: '홈런'
                });

                this.$refs.answer.focus();

                this.inputValue = '';
            }
        }
    }
</script>

<style>

</style>