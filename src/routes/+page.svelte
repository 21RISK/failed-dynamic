<script lang="ts">
	import { updated } from '$app/stores';
	import { beforeNavigate } from '$app/navigation';


    beforeNavigate(({ willUnload, to }) => {
		// Only execute if redirection is enabled
		if ($updated && !willUnload && to?.url) {
            console.log('Before navigate will reload');
			location.href = to.url.href;
		}
	});

    let answer: null | number = null;
    async function clickHandler() {
        const {mathExpert} = await import('./math-expert');
        answer = mathExpert() +1.1;
    }
</script>

<h1>Welcome to SvelteKit</h1>
<p>Let's see if we can reproduce async load error.</p>


<button on:click={clickHandler} type="button">
    Async load a Math.random!
</button>


<div>
    {answer}
</div>
