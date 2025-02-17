<template>
    <div class="container">
        <div class="text-content">
            <p>Hi Welcome to WoxWeb Online IT Academy</p>
            <h1>IT is the Future <br> IT is Business</h1>
            <TypeWriter />
            <div class="text-content-bottom">
                <p class="comment">// complete the game to continue</p>
                <p class="comment">// you can also see it on my Github page</p>
                <div class="github">
                    <p><span>const</span> <span>githubLink</span> = <span><a
                                href="#">"https://github.com/shoxrux8505"</a></span></p>
                </div>
            </div>
        </div>
        <div class="game-content">
            <div class="game-canvas">
                <SnackGame />
            </div>
        </div>
    </div>
</template>
<script>
import SnackGame from '@/components/SnackGame.vue';
import TypeWriter from '@/components/TypeWriter.vue';
export default {
    name: 'HomePage',
    components: {
        TypeWriter,
        SnackGame
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

.container {
    width: 90%;
    min-height: 60vh;
    margin: 0 auto;
    padding: 10px 30px;
    display: flex;
    align-items: center;
    justify-content: space-around;

    .text-content {
        text-align: start;
        display: flex;
        flex-direction: column;
        row-gap: 10px;

        p {
            color: var(--fff-color);
            font-size: 16px;
        }

        h1 {
            color: var(--fff-color);
            font-size: 60px;
            filter: drop-shadow(0 0 50px var(--fff-color));
        }

        .text-content-bottom {
            .comment {
                color: var(--nav-font-color);
            }

            .github {
                p {
                    span {

                        &:nth-child(1) {
                            color: var(--blue-color);
                            filter: drop-shadow(0 0 10px var(--blue-color));
                        }

                        &:nth-child(2) {
                            color: var(--green-color);
                            filter: drop-shadow(0  0 10px var(--green-color));
                        }

                        &:nth-child(3) {
                            a{
                                color: var(--orenge-color);
                                filter: drop-shadow(0 0 10px var(--orenge-color));
                            }
                        }
                    }
                }
            }
        }
    }

    .game-content {
        width: 850px;
        height: 800px;
        background: url('../components/img/blur.png');
        background-size: cover;
        padding: 10px 30px;
        display: flex;
        align-items: center;
        justify-content: center;

        .game-canvas {
            width: 510px;
            height: 475px;
            background: #01080e7f;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--fff-color);
            border-radius: 20px;
            // filter: drop-shadow(0 0 10px var(--green-color));
        }
    }

}
</style>