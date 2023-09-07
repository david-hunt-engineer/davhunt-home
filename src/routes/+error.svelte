<script>
	import Header from '$lib/components/organisms/Header.svelte';
	import Footer from '$lib/components/organisms/Footer.svelte';

	import Button from '$lib/components/atoms/Button.svelte';
	import Error from '$lib/icons/error.svelte';
</script>

<main class="page">
	<Header showBackground />
	<div class="error-page">
		<div class="container">
			<h1>Oh no!</h1>
			<div class="svg-wrapper">
				<Error />
			</div>
			<p>404 Page not found.</p>
			<br />
			<Button href="/">Start over</Button>
		</div>
	</div>
</main>

<Footer />

<style lang="scss">
	.page {
		background: var(--color--page-background);
		position: relative;
		min-height: 75vh;
	}
	.container {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		min-height: 60vh;
		text-align: center;

		.svg-wrapper {
			width: 300px;
			margin-top: -60px;
			margin-bottom: -30px;

			:global(svg) {
				filter: drop-shadow(2px 6px 0px rgba(0, 0, 0, 0.1));
			}
		}
	}
</style>
