<template>
    <div class="game-container">
        <!-- Game Screen -->
        <div class="game-screen">
            <canvas ref="gameCanvas" v-if="gameStarted"></canvas>

            <!-- Loading Screen -->
            <div v-if="!gameStarted" class="loading-screen">
                <button class="start-btn" @click="startGame">start-game</button>
            </div>
        </div>

        <!-- Game Controls -->
        <div class="game-controls">
            <p>// use keyboard <br> // arrows to play</p>
            <div class="controls">
                <button @click="changeDirection('UP')">▲</button>
                <div>
                    <button @click="changeDirection('LEFT')">◀</button>
                    <button @click="changeDirection('DOWN')">▼</button>
                    <button @click="changeDirection('RIGHT')">▶</button>
                </div>
            </div>
            <p>// food left</p>
            <div class="food-indicator">
                <span v-for="(dot, index) in foodLeft" :key="index" :class="{ active: dot }"></span>
            </div>
            <button class="skip-btn" @click="skipGame">skip</button>
        </div>

        <!-- Win Modal -->
        <div v-if="winModal" class="modal">
            <div class="modal-content">
                <h2>🎉 Congratulations! 🎉</h2>
                <p>You won the game!</p>
                <button @click="resetGame">Play Again</button>
            </div>
        </div>

        <!-- Fail Modal -->
        <div v-if="failModal" class="modal">
            <div class="modal-content">
                <h2>💀 Game Over 💀</h2>
                <p>You lost! Try again.</p>
                <button @click="resetGame">Restart</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "SnakeGame",
    data() {
        return {
            gameStarted: false,
            canvas: null,
            ctx: null,
            gridSize: 20,
            snake: [{ x: 100, y: 100 }],
            direction: "RIGHT",
            food: { x: 200, y: 200 },
            gameInterval: null,
            foodLeft: Array(10).fill(true),
            winModal: false,
            failModal: false,
        };
    },
    methods: {
        drawGame() {
            this.ctx.clearRect(0, 0, this.canvas.width, this.canvas.height);

            // Draw food
            // this.ctx.fillStyle = "#36e2a0";
            this.ctx.fillRect(this.food.x, this.food.y, this.gridSize, this.gridSize);
            this.ctx.fillStyle = "#36e2a0";
            this.ctx.beginPath();
            this.ctx.arc(
                this.food.x + this.gridSize / 2,  // Center X
                this.food.y + this.gridSize / 2,  // Center Y
                this.gridSize / 2,  // Radius
                0, Math.PI * 2
            );
            this.ctx.fill();
            this.ctx.closePath();

            // Draw snake
            this.ctx.fillStyle = "#00ff66";
            this.snake.forEach((segment, index) => {
                this.ctx.fillRect(segment.x, segment.y, this.gridSize, this.gridSize);
                if (index === 0) {
                    this.ctx.fillStyle = "#00cc55"; // Head color
                }
            });
        },
        updateGame() {
            let head = { ...this.snake[0] };

            if (this.direction === "UP") head.y -= this.gridSize;
            if (this.direction === "DOWN") head.y += this.gridSize;
            if (this.direction === "LEFT") head.x -= this.gridSize;
            if (this.direction === "RIGHT") head.x += this.gridSize;

            // Check collisions
            if (
                head.x < 0 ||
                head.y < 0 ||
                head.x >= this.canvas.width ||
                head.y >= this.canvas.height ||
                this.snake.some((segment) => segment.x === head.x && segment.y === head.y)
            ) {
                this.failModal = true;
                clearInterval(this.gameInterval);
                return;
            }

            // Add new head
            this.snake.unshift(head);

            // Eat food
            if (head.x === this.food.x && head.y === this.food.y) {
                this.spawnFood();
                this.foodLeft.pop();
                if (this.foodLeft.length === 0) {
                    this.winModal = true;
                    clearInterval(this.gameInterval);
                }
            } else {
                this.snake.pop();
            }

            this.drawGame();
        },
        spawnFood() {
            this.food = {
                x: Math.floor(Math.random() * (this.canvas.width / this.gridSize)) * this.gridSize,
                y: Math.floor(Math.random() * (this.canvas.height / this.gridSize)) * this.gridSize,
            };
        },
        changeDirection(newDirection) {
            if (
                (newDirection === "UP" && this.direction !== "DOWN") ||
                (newDirection === "DOWN" && this.direction !== "UP") ||
                (newDirection === "LEFT" && this.direction !== "RIGHT") ||
                (newDirection === "RIGHT" && this.direction !== "LEFT")
            ) {
                this.direction = newDirection;
            }
        },
        resetGame() {
            this.snake = [{ x: 100, y: 100 }];
            this.direction = "RIGHT";
            this.foodLeft = Array(10).fill(true);
            this.winModal = false;
            this.failModal = false;
            this.spawnFood();
            this.startGame();
        },
        skipGame() {
            this.resetGame();
        },
        startGame() {
            this.gameStarted = true;
            this.$nextTick(() => {
                this.canvas = this.$refs.gameCanvas;
                this.ctx = this.canvas.getContext("2d");
                this.canvas.width = 300;
                this.canvas.height = 470;
                this.spawnFood();
                this.drawGame();

                document.addEventListener("keydown", (event) => {
                    if (event.key === "ArrowUp") this.changeDirection("UP");
                    if (event.key === "ArrowDown") this.changeDirection("DOWN");
                    if (event.key === "ArrowLeft") this.changeDirection("LEFT");
                    if (event.key === "ArrowRight") this.changeDirection("RIGHT");
                });

                this.gameInterval = setInterval(this.updateGame, 150);
            });
        },
    },
    beforeUnmount() {
        clearInterval(this.gameInterval);
        document.removeEventListener("keydown", this.changeDirection);
    },
};
</script>

<style scoped>
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

/* Game Container */
.game-container {
    display: flex;
    background: #0a1e26;
    padding: 20px;
    border-radius: 12px;
    width: 500px;
    height: 470px;
    justify-content: space-between;
}

.game-controls {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
}

.game-controls .controls {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    row-gap: 5px;
    gap: 10px;

}

.game-controls .controls button {
    width: 50px;
    height: 30px;
    background: var(--dark-color);
    color: var(--fff-color);
    border: none;
    border-radius: 20px;
    cursor: pointer;
    transition: 0.5s ease;
}

.game-controls .controls button:hover {
    filter: drop-shadow(0 0 10px var(--green-color));
}

/* Loading Screen */
.loading-screen {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 470px;
    width: 300px;
    
    background: #062b33;
}

/* Modal */
.modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.7);
    display: flex;
    justify-content: center;
    align-items: center;
}

.modal-content {
    background: #062b33;
    padding: 20px;
    border-radius: 10px;
    text-align: center;
    color: white;
}

.modal-content button {
    margin-top: 10px;
    padding: 10px;
    background: #00ff66;
    border: none;
    cursor: pointer;
}

/* Start & Skip Button */
.start-btn,
.skip-btn {
    background: #ff9f43;
    border: none;
    padding: 8px 15px;
    font-size: 14px;
    margin-top: 10px;
    border-radius: 5px;
    cursor: pointer;
    font-weight: bold;
}

/* Food Indicator */
.food-indicator span {
    width: 10px;
    height: 10px;
    background: #004d33;
    border-radius: 50%;
    display: inline-block;
    margin-right: 5px;
    filter: drop-shadow(0 0 10px #00ff66);
}

.food-indicator .active {
    background: #00ff66;
}

.game-screen {
    border: 2px solid #00ff66;
    overflow: hidden;
    border-radius: 10px;
    filter: drop-shadow(0 0 5px #00ff66);
}
</style>