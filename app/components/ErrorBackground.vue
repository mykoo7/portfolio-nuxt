<!--SAME AS ANIMATED BACKGROUND FOR MAIN BUTTHIS IS FOR ERROR AND FLOATING PETALS ARE TURNED INTO COBWEBS-->
<template>
    <div class="animation-area">
        <ul class="web-area">
            <li v-for="n in 6" :key="n"></li>
        </ul>
    </div>
</template>

<style scoped>
.animation-area {
    position: fixed;
    inset: 0;
    width: 100%;
    height: 100%;
    z-index: 0;
    overflow: hidden;
    pointer-events: none;

    background: linear-gradient(
        to bottom,
        oklch(89.2% 0.058 10.001),
        oklch(81% 0.117 11.638),
        oklch(71.2% 0.194 13.428)
    );
}

.web-area {
    position: absolute;
    inset: 0;
    overflow: hidden;
}

.web-area li {
    position: absolute;
    display: block;
    list-style: none;
    background-image: url('/images/error/cobweb.png'); /* COBWEB IMAGE REPLACES THE FLOATING SQUARES */
    background-size: contain;
    background-repeat: no-repeat;
    opacity: 0.45;
    bottom: -150px;
    animation: animate 20s linear infinite;
}

.web-area li:nth-child(1) {
    left: 12%;
    width: 30px;
    height: 30px;
    animation-delay: 1.5s;
    animation-duration: 10s;
}

.web-area li:nth-child(2) {
    left: 86%;
    width: 80px;
    height: 80px;
}

.web-area li:nth-child(3) {
    left: 70%;
    width: 100px;
    height: 100px;
    animation-duration: 5.5s;
}

.web-area li:nth-child(4) {
    left: 42%;
    width: 150px;
    height: 150px;
    animation-duration: 15s;
}

.web-area li:nth-child(5) {
    left: 65%;
    width: 40px;
    height: 40px;
}

.web-area li:nth-child(6) {
    left: 15%;
    width: 110px;
    height: 110px;
    animation-duration: 3.5s;
}

@keyframes animate {
    0% {
        transform: translateY(0) rotate(0deg);
        opacity: 1;
    }

    100% {
        transform: translateY(-800px) rotate(360deg);
        opacity: 0;
    }
}
</style>