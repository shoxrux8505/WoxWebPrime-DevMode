<template>
    <div>
        <h2 ref="typewriter"></h2>
    </div>
</template>
<style lang="scss" scoped>
h2 {
    color: #4D5BCE;
    font-size: 18px;
}
</style>
<script>
import Typed from "typed.js";
export default {
    name: 'Typewriter',
    mounted() {
        this.typed = new Typed(this.$refs.typewriter, {
            strings: [">Front-end", ">Back-end", ">Javascript", ">Python", ">Diagnostics", ">Vue.js", ">React.js", ">Django", ">FastApi",],
            typeSpeed: 100,
            backSpeed: 50,
            loop: true,
        });
    },
    beforeUnmount() {
        this.typed.destroy(); // Clean up
    },
}
</script>