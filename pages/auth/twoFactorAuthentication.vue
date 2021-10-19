<template>
    <div class="flex items-center mt-10">
        <button class="text-bold bg-green-400 m-auto text-2xl p-8"
                @click="enable">Enable
        </button>
        <template v-if="openConfirm">
            <PasswordConfirmationModal :show-modal="true" @showModal="openConfirm = $event"/>
        </template>
    </div>

</template>

<script>
    import PasswordConfirmationModal from "../../components/PasswordConfirmationModal";

    export default {
        name: "twoFactorAuthentication",
        components: {PasswordConfirmationModal},
        data() {
            return {
                isEnabled: false,
                openConfirm: false,
                message: '',
                isConfirmed: false,
            }
        },

        methods: {
            async enable() {
                try {
                    await this.$axios.post('/api/user/two-factor-authentication');
                    this.isEnabled = true
                } catch (e) {
                    if (e.response.data.message) {
                        this.message = e.response.data.message;
                        this.openConfirm = true;
                    }
                }
            },
            async confirmStatus() {
                try {
                    await this.$axios.get('/api/user/confirm-password-status')
                        .then((resp) => {
                            this.isConfirmed = resp.confirmed
                        });
                } catch (e) {
                    console.log(e)
                }
            },
        }
    }
</script>

<style scoped>

</style>
