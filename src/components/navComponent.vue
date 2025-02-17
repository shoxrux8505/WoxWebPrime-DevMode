<template>
    <nav>
        <ul>
            <!-- <router-link to="/">Home</router-link> -->
            <li><a href="#">WoxWeb Prime</a></li>
            <li>
                <RouterLink to="/"><a>_hello</a></RouterLink>
            </li>
            <li>
                <RouterLink to="/about"><a>_about-me</a></RouterLink>
            </li>
            <li>
                <RouterLink to="/projects"><a>_projects</a></RouterLink>
            </li>
        </ul>
        <button>
            <RouterLink to="/contact"><a>_contact-me</a></RouterLink>
        </button>
    </nav>
</template>

<script>
import { RouterLink, RouterView } from 'vue-router'
export default {
    name: 'NavComponent',
    components: {
        // 
    }
}
</script>

<style lang="scss" scoped>
:root {
    --main-bg-color: #1E2D3D;
    --blue-color: #4D5BCE;
    --green-color: #43D9AD;
    --orenge-color: #E99287;
    --dark-orenge: #FEA55F;
    --fff-color: #FFFFFF;
    --dark-color: #01080E;
    --button-dark-color-sn: #1E2D3D;
    --nav-font-color: #607B96;
}

nav {
    width: 100%;
    border-bottom: 2px solid var(--nav-font-color);
    display: flex;
    align-items: center;
    justify-content: space-between;

    button {
        padding: 10px 28px;
        background: transparent;
        border: none;
        border-left: 2px solid var(--nav-font-color);

        a {
            color: var(--nav-font-color);
            font-size: 18px;
        }

    }

    ul {
        list-style: none;
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 20px;
        padding: 0 20px;

        li {
            padding: 10px 30px;
            border-right: 2px solid var(--nav-font-color);
            transition: 0.5s ease;

            &:nth-child(1) {
                padding: 0 50px;
                display: flex;
                align-items: center;
                justify-content: flex-start;
                padding: 10px 30px;
                border-right: 2px solid var(--nav-font-color);

                a {
                    font-size: 20px;
                    transition: 0.5s ease;

                    // &:hover {
                    //     color: royalblue;
                    //     filter: drop-shadow(0 0 10px royalblue);
                    // }
                }
            }

            a {
                color: var(--nav-font-color);
                font-size: 16px;

                // &:hover {
                //     border-bottom: 2px solid var(--dark-orenge);
                // }
            }
        }
    }
}
</style>