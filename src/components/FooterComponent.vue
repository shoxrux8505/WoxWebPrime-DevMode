<template>
    <footer>
        <ul>
            <li><a href="#">find us in:</a></li>
            <li><a href="#"><ion-icon name="logo-twitter"></ion-icon></a></li>
            <li><a href="#"><ion-icon name="logo-facebook"></ion-icon></a></li>
        </ul>
        <button><a href="#">@shoxrux8505</a><ion-icon name="logo-github"></ion-icon></button>
    </footer>
</template>
<script>
export default {
    name: 'FooterComponent',
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

footer {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
    border-top: 2px solid var(--nav-font-color);

    button {
        background: transparent;
        border: none;
        border-left: 2px solid var(--nav-font-color);
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 5px;
        font-size: 18px;
        color: var(--nav-font-color);

        a {
            padding: 10px 5px;
            color: var(--nav-font-color);
        }
    }

    ul {
        display: flex;
        align-items: center;
        justify-content: space-between;

        li {
            padding: 10px 20px;
            border-right: 2px solid var(--nav-font-color);
            display: flex;
            align-items: center;
            justify-content: center;

            a {
                font-size: 20px;
                color: var(--nav-font-color);
            }
        }
    }
}
</style>