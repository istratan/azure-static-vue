<template>
    <div>
        <div>Hello from the Azure Static Web App</div>
        <input type="text" v-model="userName" @keyup.enter="getUser" />
        <button @click="getUser" @keyup.enter="getUser">
            Load {{ userName }} github account
        </button>

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
            userName: "",
            user: {},
        };
    },

    methods: {
        getUser() {
            const self = this;
            fetch(`https://api.github.com/users/${this.userName}`)
                .then((result) => result.json())
                .then((user) => (self.user = user))
                .catch((err) => {
                    console.log(err);
                    self.alertError(
                        `GitHub account with username: ${self.userName} does not exist.`
                    );
                    self.clearState();
                });
        },

        alertError(message) {
            alert(message);
        },

        clearState() {
            this.userName = "";
            this.user = {};
        },
    },
};
</script>
