<template>
    <div>
        <h1>{{ result }}</h1>
        <form v-on:submit="onSubmitForm">
            <input ref="answer" v-model="inputValue" maxlength="4">
        </form>
        <div>
            시도: {{  }}
        </div>
    </div>
</template>

<script>
    export default{
        data() {
            return {
                inputValue: '',
                result: '',
            }
        },

        methods: {
            onSubmitForm(e) {
                e.preventDefualt();
            }
        }
    }
</script>

<style>

</style>