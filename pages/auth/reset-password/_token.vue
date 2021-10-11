<template>
    <div class="flex justify-center items-center mt-52">
        <div class="w-full max-w-md">
            <template v-if="message">
                <span class="flex justify-center text-blue-400 ">{{message}}</span>
            </template>
            <template v-else>
                <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4" @submit.prevent="submit">
                    <div class="identity-input mb-6">
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
                    <div class="password-input mb-6">
                        <label
                            for="identity"
                            class="block text-gray-700 text-sm font-bold mb-2"
                        >Password</label
                        >

                        <input
                            aria-describedby="passwordHelp"
                            v-model="form.password"

                            class="shadow appearance-none borderrounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
                            id="password"
                            type="password"
                            placeholder="*******"
                        />

                        <span class="text-xs text-red-700" id="passwordHelp"
                              v-if="errors.password">{{errors.password[0]}}</span>
                    </div>
                    <div class="password-input mb-6">
                        <label for="password_confirmation" class="block text-gray-700 text-sm font-bold mb-2">
                            Password Confirm
                        </label>

                        <input
                            aria-describedby="passwordConfirmationHelp"
                            v-model="form.password_confirmation"
                            class="shadow appearance-none borderrounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
                            id="password_confirmation"
                            type="password"
                            placeholder="*******"
                        />

                        <span class="text-xs text-red-700" id="passwordConfirmationHelp"
                              v-if="errors.password_confirmation">{{errors.password_confirmation[0]}}</span>
                    </div>

                    <div class="flex items-center justify-between">
                        <button
                            class="bg-blue-600 hover:bg-black text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
                            type="submit"
                        >
                            Submit
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
        name: "_token",
        data() {
            return {
                form: {
                    email: '',
                    token: '',
                    password: '',
                    password_confirmation: '',
                },
                errors: [],
                message: ''
            }
        },
        mounted() {
            return [
                this.form.email = this.$route.query.email,
                this.form.token = this.$route.params.token,

            ]
        },
        methods: {
            async submit() {
                try {
                    await this.$axios.$post('/api/reset-password', this.form)
                        .then((resp) => this.message = resp.message)
                    this.$router.replace('/auth/login')
                } catch (e) {
                    this.errors = e.response.data.errors
                }
            }
        }
    }
</script>

<style scoped>

</style>
