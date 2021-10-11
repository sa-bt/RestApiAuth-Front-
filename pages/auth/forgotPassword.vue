<template>
    <div class="flex justify-center items-center mt-52">
        <div class="w-full max-w-md">
            <template v-if="message">
                <span class="flex justify-center text-blue-400 ">{{message}}</span>
            </template>
            <template v-else>
                <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4" @submit.prevent="submit">
                    <div class="identity-input mb-4">
                        <label
                            for="identity"
                            class="block text-gray-700 text-sm font-bold mb-2"
                        >
                            Email</label
                        >
                        <input
                            id="identity"
                            class="shadow appearance-none borderrounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
                            type="text"
                            placeholder="Email"
                            aria-describedby="emailHelp"
                            v-model="form.email"
                        />
                        <span class="text-xs text-red-700" id="emailHelp" v-if="errors.email">{{errors.email[0]}}</span>
                    </div>

                    <div class="flex items-center justify-between">
                        <button
                            class="bg-blue-600 hover:bg-black text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
                            type="submit"
                        >
                            Send Verification Link
                        </button>
                        <NuxtLink
                            class="inline-block align-baseline font-bold text-sm text-blue-500 hover:text-blue-800"
                            :to="{name:'auth-login'}"
                        >
                            Redirect Login Page
                        </NuxtLink>
                    </div>
                </form>

            </template>
        </div>
    </div>

</template>

<script>
    export default {
        name: "forgotPassword",
        data() {
            return {
                form: {
                    email: ''
                },
                errors: [],
                message: ''
            }
        },
        methods: {
            async submit() {
                try {
                    await this.$axios.$get('sanctum/csrf-cookie')
                    await this.$axios.$post('/api/forgot-password', this.form)
                        .then((resp) => this.message = resp.message)
                } catch (e) {
                    this.errors = e.response.data.errors
                }
            }
        }
    }
</script>

<style scoped>

</style>
