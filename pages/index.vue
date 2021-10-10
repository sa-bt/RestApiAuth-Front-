<template>
    <div class="bg-cover max-h-screen w-full" style="background-image: url('10.jpg')">
        <div class="flex flex-col justify-between min-h-screen">
            <div class="flex-1 flex flex-col justify-center items-start space-y-4 ml-10">
                <h1 class="text-3xl">Welcome to PHPwithSABT</h1>
                <div class="flex space-x-12">
                    <NuxtLink to="auth/register" class="text-2xl hover:text-blue-500">Register</NuxtLink>
                    <NuxtLink to="auth/login" class="text-2xl hover:text-blue-500">Login</NuxtLink>


                </div>
            </div>
            <!--            <div class="flex-1 flex items-end mb-10 ml-10">-->

            <!--            </div>-->

        </div>
    </div>
</template>

<script>
    export default {}
</script>
