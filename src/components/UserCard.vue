<template>
    <div>
        <font-awesome-icon icon="fa-solid fa-spinner" class="anim-spinner"
            v-if="!this.photo" />
        <div class="cardContainer"
            v-if="this.photo" >
            <img :src="getPhoto" />
            <ul>
                <li>
                    <h3>Name</h3>
                    <h1>{{this.name}}</h1>
                </li>
                <li>
                    <h3>Email</h3>
                    <h1>{{this.email}}</h1>
                </li>
                <li>
                    <h3>Age</h3>
                    <h1>{{this.age}}</h1>
                </li>
                <li>
                    <h3>Country</h3>
                    <h1>{{this.country}}</h1>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
    export default {
        name: "UserCard",
        data(){
            return{
                photo: "",
                name: "",
                email: "",
                age: "",
                country: ""
            }
        },
        methods: {
            getUser: function () {
                fetch('https://randomuser.me/api/')
                .then((response) => response.json())
                .then((data) => data.results[0])
                .then((user) => {
                    this.photo = user.picture.large
                    this.name = `${user.name.first} ${user.name.last}`
                    this.email = user.email
                    this.age = user.dob.age
                    this.country = user.location.country
                })
            }
        },
        computed: {
            getPhoto(){
                return this.photo
            }
        },
        beforeCreate(){
            console.log('lifecycle hook: beforeCreated')
        },
        created(){
            console.log('lifecycle hook: created')
        },
        beforeMount(){
            console.log('lifecycle hook: beforeMount')
        },
        mounted(){
            console.log('lifecycle hook: mounted')
            this.getUser()

        },
        beforeUpdate(){
            console.log('lifecycle hook: beforeUpdate')
        },
        updated(){
            console.log('lifecycle hook: updated')
        },
        beforeUnmount(){
            console.log('lifecycle hook: beforeUnmount')
        },
        unmounted(){
            console.log('lifecycle hook: unmounted')
        }
    }
</script>

<style scoped>
    @keyframes spin {
        from {
            transform:rotate(0deg);
        }
        to {
            transform:rotate(360deg);
        }
    }
    .anim-spinner{
        animation: spin 1.5s linear infinite;
        font-size: 2rem;
    }
    .cardContainer{
        padding-top: 50px;
        padding-bottom: 50px;
    }
    img{
        height: 150px;
        width: 150px;
        border: 0.5px solid var(--titlecolor);
        border-radius: 50%;
        margin-bottom: 10px;
        box-shadow: var(--backgroundcolor) 0 0 15px 1px;
    }
    ul{
        padding: 0;
        margin: 0;
        text-align: left;
        list-style: none;
    }
    li{
        border-bottom: 1px solid;
        padding-left: 5px;
        padding-right: 5px;
    }
    h3{
        color: var(--titlecolor);
    }
    h1{
        font-size: 1.5rem;
    }
</style>