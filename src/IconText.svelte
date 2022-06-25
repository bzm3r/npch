<script>
    export let text = "";
    export let icon = "";
    let src = "/assets/" + icon + ".svg";
</script>

<div class="icon">
    <img class="iconImage" {src} alt={icon} title={icon}>
    <div class="iconText">{text}</div>
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
    transform: translate(-50%, -60%);
    z-index: 1;
    }
</style>

