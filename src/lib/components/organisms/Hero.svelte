<script>
	import FeaturesIcon from '$lib/icons/features.svelte';
	import GitHubIcon from '$lib/icons/socials/github.svelte';
	import Button from '$lib/components/atoms/Button.svelte';
	import Sparkles from '../atoms/Sparkles.svelte';
	import Socials from '$lib/components/molecules/Socials.svelte';
	import Image from '../atoms/Image.svelte';
</script>

<section id="hero">
	<h1 class="hello">Hello there.</h1>
	<p class="intro">
		I'm David Hunt, a <Sparkles>Data Scientist</Sparkles> from Wellington, New Zealand.
	</p>
	<Socials />
</section>

<style lang="scss">
	@import '$lib/scss/breakpoints.scss';

	#hero {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		gap: 15px;
		position: relative;
		padding: 80px 0;

		@include for-phone-only {
			padding: 40px 0 50px;
		}

		.hello {
			text-align: center;
			font-weight: 1000;
			color: rgba(0, 0, 0, 0.6);
		}

		.intro {
			text-align: center;
			font-weight: 500;
			font-size: 1.4rem;
			width: min(100%, 480px);
			display: flex;
			flex-direction: column;
			color: rgba(0, 0, 0, 0.7);

			.left {
				text-align: left;
			}
			.right {
				text-align: right;
			}

			@include for-phone-only {
				display: none;
			}
		}

		.ctas {
			display: flex;
			flex-wrap: wrap;
			align-items: center;
			justify-content: center;
			gap: 10px;
			width: 100%;
		}
	}
</style>
