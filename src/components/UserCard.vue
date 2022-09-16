<template>
    <div>
        <font-awesome-icon icon="fa-solid fa-spinner" class="anim-spinner"
            v-if="!this.photo" />
        <div class="cardContainer"
            v-if="this.photo" >
            <img :src="getPhoto" :class="isFemaleCSSClass"/>
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
                country: "",
                isFemale: false
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
                    this.isFemale = (user.gender == 'female') ? true : false
                })
            }
        },
        computed: {
            getPhoto(){
                return this.photo
            },
            isFemaleCSSClass(){
                return (this.isFemale) ? "female" : ""
            }
        },
        beforeCreate(){

        },
        created(){

        },
        beforeMount(){

        },
        mounted(){

            this.getUser()

        },
        beforeUpdate(){

        },
        updated(){

        },
        beforeUnmount(){

        },
        unmounted(){

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
    @keyframes pulsing{
        from{ box-shadow: var(--textcolor) 0 0 10px 1px; }
        to{ box-shadow: var(--textcolor) 0 0 15px 5px; }
    }
    img{
        height: 150px;
        width: 150px;
        border: 0.5px solid var(--titlecolor);
        border-radius: 50%;
        margin-bottom: 10px;
        animation: pulsing alternate-reverse infinite 1.2s linear;
    }
    img.female{
        box-shadow: var(--secondarycolor) 0 0 20px 2px;
        animation: none;
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