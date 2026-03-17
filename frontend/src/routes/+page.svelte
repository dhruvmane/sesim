<style>
    @import url('https://fonts.googleapis.com/css2?&family=DM+Mono:ital,wght@0,300;0,400;0,500;1,300;1,400;1,500&family=Google+Sans+Code:ital,wght@0,300..800;1,300..800');
    @import url('https://fonts.googleapis.com/css2?family=Six+Caps&disbutton=swap');

    * {
        text-align: center;
    }

    .title {
        font-family: 'Six Caps';
        font-size: 100px;
        margin: 0em;
        margin-top: 30vh;
    }
    .subtitle {
        font-family: 'Google Sans Code';
        font-size: 25px;
        margin: 0em;
    }
    .menu {
        margin: 0;
        margin-top: 3vh;
    }
    .button {
        font-family: 'Google Sans Code';
        display: inline-block;
        height: 40px;
        width: 150px;
        font-size: 20px;
        background-color: #365096;
        color: #d2c8ffab;
        margin-bottom: 10px;
        border-radius: 10px;
        transition: 0.05s ease;
    }

    .smallbutton {
        font-family: 'Google Sans Code';
        height: 40px;
        width: 75px;
        font-size: 30px;
        background-color: #365096;
        color: #d2c8ffab;
        margin-bottom: 10px;
        border-radius: 10px;
        transition: 0.05s ease;
    }
    
    
    .button:hover {
        color: white;
        transition: 0.05s ease;
        z-index: -1;
        border: 2px black;
        border-style: solid;
    }

    .smallbutton:hover {
        color: white;
        transition: 0.05s ease;
        z-index: -1;
        border: 2px black;
        border-style: solid;
    }

    @keyframes blinking{
        0% {opacity: 100%}
        50% {opacity: 0%}
        100% {opacity: 100%}
    }
    .caret {
        animation: blinking 0.7s ease-in-out 1s infinite;
    }

    .menuButtonIcon {
        margin: 0em;
        padding: 0em;
        height: 25px;
    }

</style>
<script lang="ts">
    import { redirect, type text } from "@sveltejs/kit";
    import hoverSound from '$lib/sounds/hover.mp3';
    import githubIcon from '$lib/assets/icons/github.svg';
    import homeIcon from '$lib/assets/icons/home.svg';
    //@ts-nocheck

    let subtitle_typewriter = $state("")
    async function animate_typewriter(text: string, variable: string, timeVar: number) {
        let animateField = ""
        let indices = text.length;
        let index = 0;

        // Animation
        const animation = setInterval(() => {          
            // Add Text
            if (index <= indices) {
                animateField += text[index]
                subtitle_typewriter = animateField
                index++;
            }
            // console.log(`indices: ${indices}, index: ${index}`)

            // Stop Animation once All Text has been Appended
            if (index == indices) {
                clearInterval(animation);
            }
        }, timeVar)
    }

    animate_typewriter("a Stock Exchange Simulator.", subtitle_typewriter, 100)

    function buttonHover() {
        const hoverSound = document.getElementById('hoverSound') as HTMLAudioElement;
        hoverSound.currentTime = 0;
        hoverSound.play();
    }

    function workInProgress() {
        throw redirect(303, '/wip')
    }

</script>
<main>
    <title>SESIM</title>
    <!--Title-->
    <div>
        <p class="title">SESIM</p>
        <div>
            <p class="subtitle">{subtitle_typewriter}<span class="caret">|</span></p>
        </div>
    </div>
    <!--Main Menu Buttons-->
    <div class="menu">
        <audio id=hoverSound src={hoverSound}></audio>
        <div>
            <button onclick={workInProgress} onmouseenter={buttonHover} class="button">PLAY</button>
        </div>
        <div>
            <button onclick={workInProgress} onmouseenter={buttonHover} class="button">OPTIONS</button>
        </div>
        <div>
            <button onclick={workInProgress} onmouseenter={buttonHover} class="smallbutton" title="github"><img class="menuButtonIcon" src={githubIcon} alt="github"></button>
            <button onclick={workInProgress} onmouseenter={buttonHover} class="smallbutton" title="github"><img class="menuButtonIcon" src={homeIcon} alt="github"></button>
        </div>
    </div>
</main>