<script>
	import { onMount } from 'svelte';
	let time = new Date();

	$: hours = String(time.getHours()).padStart(2, "0");
	$: minutes = String(time.getMinutes()).padStart(2, "0");
	$: seconds = String(time.getSeconds()).padStart(2, "0");

	onMount(() => {
		const interval = setInterval(() => {
			time = new Date();
			document.querySelector("div.running-border").setAttribute('data-content', `${hours}:${minutes}:${seconds}`);
		}, 1000);
		return () => {
			clearInterval(interval);
		};
	});

</script>
<div class="running-border">
</div>
<style>
    div.running-border {
        width: 200px;
        height: 200px;
        box-shadow: 16px 14px 20px #0000008c;
        border-radius: 10px;
        position: relative;
        overflow: hidden;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    div.running-border::before{
        content: '';
        background-image: conic-gradient(
            #ff0052 20deg,
            transparent 120deg
        );
        width: 150%;
        height: 150%;
        position: absolute;
        animation: rotate 2s linear infinite;
    }
    div.running-border::after{
        content: attr(data-content);
        width: 190px;
        height: 190px;
        background: #101010;
        position: absolute;
        border-radius: 10px;
        display: flex;
        justify-content: center;
        align-items: center;
        color: #ff0052;
        font-size: larger;
        letter-spacing: 5px;
        box-shadow: inset 20px 20px 20px #0000008c;
    }
    @keyframes rotate {
        0%{
            transform: rotate(0deg);
        }
        100%{
            transform: rotate(-360deg);
        }
    }
</style>

