<script>
import {onMount} from 'svelte';
import Button from './Button.svelte';
import {observer, setObserver} from '../store.js';

let scrollY, header, div;

let addY = () => {};
onMount(() => {
	addY = () => {
		if(scrollY<=window.innerHeight){
			div.style.marginTop = (scrollY*0.7)+'px';
			header.style.backgroundPosition = "left, 50% "+(scrollY-40)+"px, right";
		}
	}
	setObserver();
	observer.observe(header);
});

$: addY(scrollY);
</script>

<style>
header {
	height: 100vh;
	background-image: linear-gradient(45deg, #000022, #44442277), url(../bg.jpg), linear-gradient(#000022, #000022);
	background-repeat: no-repeat, no-repeat;
	background-position: left, center, right;
	background-size: cover, cover, cover;
	color: #eeeeee;
	display: flex;
	align-items: center;
	justify-content: center;
	user-select: none;
	overflow: hidden;
}
div {
	padding: 1rem;
	text-align: center;
}
h1 {
	font-weight: normal;
	cursor: pointer;
}
</style>

<svelte:window bind:scrollY={scrollY}></svelte:window>
<header id="hero" bind:this={header}>
	<div bind:this={div}>
		<h1>Hello, I'm Sameer Tariq.</h1>
		<h1>I'm a full-stack web developer.</h1>

		<Button target='about' text='About Me' color="#eeeeee" />
	</div>
</header>