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
                isDark: this.getThemeFromLS()
            }
        },
        methods: {
            getThemeFromLS: function(){
                const savedTheme = localStorage.getItem('darkmode')
                if(savedTheme === null || savedTheme === undefined) return true
                return (savedTheme == 'true') ? true : false
            },
            toggleDark: async function (){
                console.log('Toggling', this.isDark)
                const classToAddToRoot = await (this.isDark) ? "" : "lightmode"
                console.log("root class", classToAddToRoot)
                document.documentElement.className = await classToAddToRoot
            },
            setThemeOsLS: function(){
                localStorage.setItem('darkmode', this.isDark);
            }
        },
        watch:{
            isDark(){
                this.toggleDark()
                this.setThemeOsLS()
            }
        },
        computed: {
            isDarkClass(){
                return (this.isDark) ? "toggled" : null
            }
        },
        beforeCreate(){},
        created(){},
        beforeMount(){},
        mounted(){
            this.toggleDark()
            this.setThemeOsLS()
        },
        beforeUpdate(){},
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