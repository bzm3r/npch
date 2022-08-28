<script>
    export let text = "";
    export let icon = "";
    let src = "/assets/" + icon + ".svg";
    let iconY = {
        atk: 65,
        def: 60,
        fort: 60,
        hp: 65,
        init: 90,
        ref: 60,
        skl: 60,
        will: 60,
    }
</script>

<div class="icon">
    <img class="iconImage" {src} alt={icon} title={icon}>
    <div class="iconText" style:--y="-{iconY[icon]}%">{text}</div>
</div>

<style>
	.icon {
    position: relative;
    text-align: center;
    color: black;
    }

    .iconImage {
        z-index: 0;
    }

    .iconText {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, var(--y));
    z-index: 1;
    font-weight: bold;
    }
</style>

