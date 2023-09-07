<script>
	import FooterWave from '$lib/icons/footer-wave.svelte';
	import Socials from '$lib/components/molecules/Socials.svelte';
	import ThemeToggle from '$lib/components/molecules/ThemeToggle.svelte';
	import RssLink from '$lib/components/atoms/RssLink.svelte';
</script>

<footer>
	<div class="wave2">
		<FooterWave />
	</div>
	<div class="content">
		<div class="socials">
			<Socials />
			<!-- <RssLink /> -->
			<ThemeToggle />
		</div>
	</div>
	<!-- <Spacer /> -->
</footer>

<style lang="scss">
	footer {
		.wave2 {
			// width: 100%;
			// height: 120;
			// viewbox: '0 0 1440 120';
			// fill: none;
		}
		min-height: 25vh;

		width: 100%;
		background: linear-gradient(
			60deg,
			var(--color--waves-start-footer) 0%,
			var(--color--waves-end-footer) 100%
		);
		display: grid;
		grid-template-rows: 120px 1fr;

		.content {
			display: flex;
			// height: 100vh;
			flex-direction: column;
			align-items: center;
			justify-content: center;
			gap: 15px;
			font-weight: 600;
			text-align: center;

			.credits {
				font-weight: 400;
				font-size: 90%;
				color: var(--color--text-shade);
			}

			.socials {
				display: flex;
				align-items: center;
				gap: 20px;
			}
		}

		a {
			&:hover {
				filter: drop-shadow(0px 0px 3px var(--color--primary));
			}
		}
	}
</style>
