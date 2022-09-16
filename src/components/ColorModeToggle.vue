<template>
    <div class="dm-toggle-container" :class="(isDarkClass)">
        <input 
            type="checkbox" 
            id="dm-toggle"
            v-model="isDark"
            >
    </div>
</template>

<script>
export default {
    name: "UserCard",
        data(){
            return{
                isDark: true,
            }
        },
        methods: {
            toggleDark: function (){
                document.documentElement.className = (document.documentElement.classList.contains('lightmode')) ? "" : "lightmode"
            }
        },
        computed: {
            isDarkClass(){
                return this.isDark ? "toggled" : null
            }
        },
        beforeCreate(){},
        created(){},
        beforeMount(){},
        mounted(){},
        beforeUpdate(){
            this.toggleDark()
        },
        updated(){},
        beforeUnmount(){},
        unmounted(){}
}
</script>

<style scoped>
    .dm-toggle-container{
        --height: 25px;
        height: var(--height);
        width: 45px;
        padding: 0;
        margin: 0;
        background-color: var(--backgroundcolor);
        border: var(--textcolor) solid 0.5px;
        border-radius: var(--height);
        display: flex;
        align-items: center;
        justify-content: flex-start;
    }
    input{
        appearance: none;
        margin: 0 3px;
        padding: 0;
        cursor: pointer;
        height: 18px;
        width: 18px;
        border-radius: 50%;
        background-color: var(--titlecolor);
    }
    .dm-toggle-container.toggled{
        justify-content: flex-end;
    }
</style>