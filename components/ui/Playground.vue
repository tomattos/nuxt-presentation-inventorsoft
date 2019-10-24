<template>
  <div class="playground">
    <canvas ref="playground" width="400" height="400"></canvas>
  </div>
</template>

<script>
    export default {
        name: "Playground",
        data() {
            return {
                ctx: null,
                imgPosition: null,
                startTime: null
            }
        },
        computed: {
            score() {
                return Date.now() - this.startTime;
            }
        },
        methods: {
            init() {
                this.startTime = Date.now();
                /* clear canvas */
                this.ctx !== null && this.ctx.clearRect(0, 0, 400, 400);
                this.ctx = this.$refs.playground.getContext('2d');

                /* draw playground */
                this.ctx.strokeRect(0, 0, 400, 400);

                for (let i = 1; i <= 3; i++) {

                    for (let j = 1; j <= 3; j++) {
                        let x = 100 * j;
                        let y = 100 * i;

                        this.ctx.beginPath();
                        this.ctx.arc(x, y, 40, 0, Math.PI * 2, false);
                        this.ctx.stroke();
                    }
                }

                /* animate animal */
                let interval = setInterval(() => {
                    const x = 100 * this.getRange(1, 4) - 25;
                    const y = 100 * this.getRange(1, 4) - 25;

                    this.imgPosition !== null && this.ctx.clearRect(this.imgPosition.x, this.imgPosition.y, 50, 50);
                    this.drawAnimal(x, y);
                    this.imgPosition = {x, y};
                }, 1000);

                /* handle kick */
                this.$refs.playground.addEventListener('click', (e) => {
                    let x = e.layerX;
                    let y = e.layerY;

                    if (x >= this.imgPosition.x && x <= this.imgPosition.x + 50 &&
                        y >= this.imgPosition.y && y <= this.imgPosition.y + 50) {
                        clearInterval(interval);

                        this.$root.$emit('bv::show::modal', 'CongradModal');
                    }
                })
            },

            drawAnimal(x, y) {
                const img  = new Image();
                img.onload = () => {
                    this.ctx.drawImage(img, x, y, 50, 50);
                };
                img.style.border = '1px solid #000';
                img.src = require('~/assets/images/humster.png');

                this.imgPosition = { x, y };
            },

            getRange(min, max) {
                min = Math.ceil(min);
                max = Math.floor(max);
                return Math.floor(Math.random() * (max - min)) + min;
            },

            updateScore(score) {
                const gamers = JSON.parse(localStorage.getItem('gamers'));
                const currentGamer = gamers.pop();
                currentGamer.score = score;
                localStorage.setItem('gamers', JSON.stringify([...gamers, currentGamer]));
            }
        },
        mounted() {
            this.init();

            this.$root.$on('oneMoreTime', () => {
                this.updateScore(this.score);
                this.init();
            })
        }
    }
</script>

<style scoped>
  .playground {
    height: calc(100vh - 86px);
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: url("../../assets/images/hammer.png"), auto;
  }
</style>
