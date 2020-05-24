<template>
    <div class="wrap">
        <div class="digital">
            <div class="digital-text">
                <h2> {{ time }} </h2>
            </div>
        </div>
        <div class="clock">
            <div class="centerpoint"></div>
            <div class="hour"></div>
            <div class="minute"></div>
            <div class="second"></div>
        </div>
        <div class="pyro">
            <div class="before"></div>
            <div class="after"></div>
        </div>
    </div>
</template>
<style lang="scss" scope>
    @import url("https://fonts.googleapis.com/css2?family=Titillium Web");
    @mixin lowheight() {
        @media (max-height: 300px) {
            @content;
        }
    }

    @mixin midheight() {
        @media (min-height: 301px) and (max-height: 700px) {
            @content;
        }
    }
    $border: #236045;
    * {
        margin: 0;
        padding: 0;
        font-family: Titillium Web;

    }
    body {
        background: rgba(0, 40, 40, 50%);
        overflow: hidden;
    }
    .wrap {
        height: 100vh;
        width: 100vw;
    }
    .clock {
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        width: 200px;
        height: 200px;
        border: 3px solid $border;
        border-radius: 100px;
        background: linear-gradient(-45deg, #445566, #448855, #55ee44);
        margin: auto;
        transition: all .2s;
        @include lowheight {
            transform: translateY(10%);
        }
    }
    .centerpoint {
        background: #000;
        position: absolute;
        width: 10px;
        height: 10px;
        border-radius: 5px;
        top: 0;
        right: 0;
        left: 0;
        bottom: 0;
        margin: auto;
    }
    $wid: 7px;
    .hour {
        position: absolute;
        width: $wid;
        height: 60px;
        background: #88dd88;
        top: -35px;
        left: -1px;
        right: 0;
        bottom: 0;
        margin: auto;
        transform-origin: 50% 80%;
    }
    .minute {
        position: absolute;
        width: $wid/1.5;
        height: 90px;
        background: #446553;
        transform-origin: 50% 80%;
        top: -54px;
        left: -1px;
        right: 0;
        bottom: 0;
        margin: auto;
        transform: rotate(90deg);
    }
    .second {
        position: absolute;
        width: $wid/2;
        height: 110px;
        background: #504433;
        transform-origin: 50% 80%;
        top: -70px;
        left: -1px;
        right: 0;
        bottom: 0;
        margin: auto;
        transform: rotate(250deg);
    }
    .digital {
        position: fixed;
        width: 100vw;
        text-align: center;
        top: 30%;
        transition: all .2s;
        .digital-text {
            position: absolute;
            width: 150px;
            transform: translate(50%);
            border: 1px dotted #444;
            background: #203433;
            color: #eee;
            right: 50%;

            @include lowheight {
                top: 0;
            }
        }
        @include lowheight {
            top: 0;
            margin-top: 1%;
        }
    }

    $particles: 50;
    $width: 500;
    $height: 500;

    // Create the explosion...
    $box-shadow: ();
    $box-shadow2: ();
    @for $i from 0 through $particles {
    $box-shadow: $box-shadow,
                random($width)-$width / 2 + px
                random($height)-$height / 1.2 + px
                hsl(random(360), 100, 50);
    $box-shadow2: $box-shadow2, 0 0 #fff
    }
    @mixin keyframes ($animationName) {
        @-webkit-keyframes #{$animationName} {
            @content;
        }

        @-moz-keyframes #{$animationName} {
            @content;
        }

        @-o-keyframes #{$animationName} {
            @content;
        }

        @-ms-keyframes #{$animationName} {
            @content;
        }

        @keyframes #{$animationName} {
            @content;
        }
    }

    @mixin animation-delay ($settings) {
        -moz-animation-delay: $settings;
        -webkit-animation-delay: $settings;
        -o-animation-delay: $settings;
        -ms-animation-delay: $settings;
        animation-delay: $settings;
    }

    @mixin animation-duration ($settings) {
        -moz-animation-duration: $settings;
        -webkit-animation-duration: $settings;
        -o-animation-duration: $settings;
        -ms-animation-duration: $settings;
        animation-duration: $settings;
    }

    @mixin animation ($settings) {
        -moz-animation: $settings;
        -webkit-animation: $settings;
        -o-animation: $settings;
        -ms-animation: $settings;
        animation: $settings;
    }

    @mixin transform ($settings) {
        transform: $settings;
        -moz-transform: $settings;
        -webkit-transform: $settings;
        -o-transform: $settings;
        -ms-transform: $settings;
    }

    /* body {
    margin:0;
    padding:0;
    background: #000;
    overflow: hidden;
    } */
    .pyro {
        display: none;
        position: fixed;
        float: center;
        width: 100vw;
        height: 100vh;
    }
    .pyro > .before, .pyro > .after {
        position: absolute;
        width: 5px;
        height: 5px;
        border-radius: 50%;
        box-shadow: $box-shadow2;
        @include animation((1s bang ease-out infinite backwards, 1s gravity ease-in infinite backwards, 5s position linear infinite backwards));
    }
        
    .pyro > .after {
        @include animation-delay((1.25s, 1.25s, 1.25s));
        @include animation-duration((1.25s, 1.25s, 6.25s));
    }
            
    @include keyframes(bang) {
        to {
            box-shadow:$box-shadow;
        }
    }
        
    @include keyframes(gravity)  {
        to {
            @include transform(translateY(200px));
            opacity: 0;
        }
    }
        
    @include keyframes(position) {
        0%, 19.9% {
            margin-top: 10%;
            margin-left: 40%;
        }
        20%, 39.9% {
            margin-top: 40%;
            margin-left: 30%;
        }
        40%, 59.9% {  
            margin-top: 20%;
            margin-left: 70%
        }
        60%, 79.9% {  
            margin-top: 30%;
            margin-left: 20%;
        }
        80%, 99.9% {  
            margin-top: 30%;
            margin-left: 80%;
        }
    }
</style>
<script>
export default {
    name: 'mainclock',
    data (){
        return {
            time: null,
            baseDate: new Date('2019/03/20'),
        }
    },
    created() {
        this.timeAction();
    },
    methods: {
        timeAction () {
            setInterval( () => {
                let nowTime = new Date();
                let hour = nowTime.getHours() > 12 ? nowTime.getHours() - 12 : nowTime.getHours();
                let min = nowTime.getMinutes();
                let sec = nowTime.getSeconds();
                let ampm = nowTime.getHours() >= 12 ? 'PM' : 'AM';
                document.querySelector('.hour').style.transform =  `rotate(${(hour * 30) + (0.5 * min)}deg)`;
                document.querySelector('.minute').style.transform = `rotate(${min * 6}deg)`;
                document.querySelector('.second').style.transform = `rotate(${sec * 6}deg)`;
                this.time = `${hour > 9 ? hour : "0" + hour}:${min>9 ? min : "0" + min}:${sec > 9 ? sec : "0" + sec} ${ampm}`;
            }, 1000);
            setInterval( () => {
                this.monthDiff(nowTime);
            }, 1000*360*6)
        },
        monthDiff(fromDate) {
            let celebrateDay = fromDate.getMonth() - this.baseDate.getMonth() + (12 * (fromDate.getFullYear() - this.baseDate.getFullYear()));
            let dis = document.querySelector('.pyro').style.display;
            console.log(dis)
            if (fromDate.getDate() == 10 && !dis) {
                document.querySelector('.pyro').style.display = "block";
                setTimeout(()=>{
                    document.querySelector('.pyro').style.display = "none";
                }, 2000)
            }
        }
    }
}
</script>