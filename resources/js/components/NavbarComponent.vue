<template>
    <section class="border border-gray-400 pb-5">
        <div class="nav-bar mt-4 container mx-auto">
            <div class="flex items-center justify-between">
                <router-link to="/">
                    <img src="/images/logo.png" alt="logo">
                </router-link>

                <search-component></search-component>

                <div class="flex">
                    <button class="rounded-icon"><i class="las la-shopping-bag"></i></button>
                    <div class="relative">
                        <button  v-if="isAuthenticated" @click="showAccMenu = !showAccMenu" class="rounded-icon ml-4 "><i class="lar la-user"></i></button>
                        <div v-show="showAccMenu" class="bg-white absolute shadow-xl w-64 rounded" style="top: 100%">
                            <ul class="flex-col">
                                <li><a href="#" class="px-2 py-3 border-b border-gray-300 hover:bg-gray-200 block">Password</a></li>
                                <li><a href="#" class="px-2 py-3 border-b border-gray-300 hover:bg-gray-200 block">Address Book</a></li>
                                <li><a href="#" class="px-2 py-3 border-b border-gray-300 hover:bg-gray-200 block">Update Profile</a></li>
                                <li><a href="#" @click="logout" class="px-2 py-3 hover:bg-gray-200 block">Sign Out</a></li>
                            </ul>
                        </div>
                    </div>

                    <div class="flex flex-col ml-3 justify-center">
                        <p v-if="isAuthenticated" class="text-gray-600 text-sm">Welcome {{ $store.state.user.name }}!</p>
                        <div class="text-sm">
                            <router-link v-if="!isAuthenticated" to="/login" class="link uppercase font-bold">Sign in</router-link>
                            <a href="#" @click="logout" class="link" v-if="isAuthenticated">Logout</a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
export default {
    name: "NavbarComponent",
    data() {
        return {
            showAccMenu: false
        }
    },
    computed: {
        isAuthenticated() {
            return this.$store.state.user != '';
        }
    },
    methods: {
        logout() {
            axios.post('/logout')
            .then(() => {
                window.location.replace('/')
            })
            .catch((message) => {
                console.log(error.message)
            })
        }
    }
}
</script>
