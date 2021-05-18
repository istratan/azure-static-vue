<template>
    <div>
        <div>Hello from the Azure Static Web App</div>
        <button @click="getUser">Load user</button>

        <div v-if="user && user.name">
            <img :src="user.avatar_url" :alt="user.name" />
            <p>{{ user.login }}</p>
        </div>
    </div>
</template>

<script>
export default {
    name: "App",
    data() {
        return {
            value: "World",
            user: {},
        };
    },

    methods: {
        getUser() {
            fetch("https://api.github.com/users/istratan")
                .then((result) => result.json())
                .then((user) => (this.user = user));
        },
    },
};
</script>
