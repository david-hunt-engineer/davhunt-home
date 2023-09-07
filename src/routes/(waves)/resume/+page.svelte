<script lang="ts">
	import BlogPostCard from '$lib/components/molecules/BlogPostCard.svelte';
	import ContentSection from '$lib/components/organisms/ContentSection.svelte';
	import type { BlogPost } from '$lib/utils/types';

	export let data: {
		posts: BlogPost[];
	};

	let { posts } = data;
</script>

<div class="container">
	<ContentSection title="All Blog Posts">
		<div class="timeline-container">
			<div class="timeline-line" />
			<div class="timeline-content">
				{#each posts as post}
					<div class="timeline-item">
						<!-- <svg class="connector-line">
							<!-- Draw the smooth, wavy bezier curve with scale
							<path
								d="M 5 5 C 85 5 50 22 150 20"
								stroke="#4d4d4d"
								fill="transparent"
								stroke-width="2"
								transform="scale(1, 1)"
							/>
							<!-- Draw the node as a circle at the end of the curve with scale
							<circle cx="5" cy="5" r="5" fill="black" transform="scale(1, 1)" />
						</svg> -->

						<svg class="connector-line">
							<defs>
								<linearGradient id="gradient" x1="0%" y1="0%" x2="100%" y2="100%">
									<stop offset="0%" style="stop-color:lightblue;stop-opacity:1" />
									<stop offset="100%" style="stop-color:lightpink;stop-opacity:1" />
								</linearGradient>
							</defs>
							<!-- Fill SVG background with gradient -->
							<!-- <rect x="0" y="0" width="100%" height="100%"  /> -->

							<!-- Draw the smooth, wavy bezier curve
							<path
								d="M 110 0 C 30 0 86 52 0 50 C 86 50 50 150 110 150 Z"
								stroke="#4d4d4d"
								stroke-width="0"
								fill="url(#gradient)"
								transform="scale(1, 1)"
							/> -->

							<path
								d="M 5 5 C 83 0 32 143 145 145"
								stroke="#4d4d4d"
								stroke-width="2"
								fill="transparent"
								transform="scale(1, 1)"
							/>
							<!-- Draw the node as a circle at the end of the curve -->
							<circle cx="5" cy="5" r="5" fill="#4d4d4d" transform="scale(1, 1)" />
							<circle cx="145" cy="145" r="5" fill="#4d4d4d" transform="scale(1, 1)" />
						</svg>
						<BlogPostCard
							title={post.title}
							coverImage={post.coverImage}
							excerpt={post.excerpt}
							readingTime={post.readingTime}
							slug={post.slug}
							tags={post.tags}
						/>
					</div>
				{/each}
			</div>
		</div>
	</ContentSection>
</div>

<style lang="scss">
	.timeline-container {
		display: flex;
		align-items: flex-start;
		position: relative;
	}

	.timeline-line {
		height: 100%;
		width: 2px;
		background-color: #4d4d4d;
		position: absolute;
		top: 0;
		left: 34px;
	}

	.timeline-content {
		flex-grow: 1;
		margin-left: 30px; /* Increased margin-left for more right positioning */
	}

	.connector-line {
		position: absolute;
		top: 0;
		left: 0;
		width: 150px;
		height: 150px;
		z-index: 1;
	}

	.timeline-item {
		position: relative;
		margin-bottom: 40px;
	}

	.timeline-point {
		width: 16px;
		height: 16px;
		background-color: #ccc;
		border-radius: 50%;
		position: absolute;
		left: -28px;
		top: 0;
	}

	/* Add these to resize BlogPostCard */
	.timeline-item > :global(.blog-post-card) {
		width: 70%; /* Reduced width */
		margin-left: auto; /* Aligns card to the right */
	}
</style>
