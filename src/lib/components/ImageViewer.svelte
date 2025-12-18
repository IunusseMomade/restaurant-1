<script>
	import { X, ChevronLeft, ChevronRight } from '@lucide/svelte';
	
	let { images = [], onClose, initialIndex = 0 } = $props();
	let currentIndex = $state(0);

	$effect(() => {
		const maxIndex = (images?.length ?? 0) - 1;
		if (maxIndex < 0) {
			currentIndex = 0;
			return;
		}
		const nextIndex = Math.min(Math.max(Number(initialIndex) || 0, 0), maxIndex);
		currentIndex = nextIndex;
	});

	/** @param {any=} e */
	function next(e) {
		e?.stopPropagation();
		if (!images?.length) return;
		currentIndex = (currentIndex + 1) % images.length;
	}

	/** @param {any=} e */
	function prev(e) {
		e?.stopPropagation();
		if (!images?.length) return;
		currentIndex = (currentIndex - 1 + images.length) % images.length;
	}

	/** @param {KeyboardEvent} e */
	function handleKeydown(e) {
		if (e.key === 'ArrowRight') next();
		if (e.key === 'ArrowLeft') prev();
		if (e.key === 'Escape') onClose();
	}
</script>

<svelte:window onkeydown={handleKeydown} />

<!-- svelte-ignore a11y_click_events_have_key_events -->
<!-- svelte-ignore a11y_no_noninteractive_element_interactions -->
<div 
	class="image-viewer-overlay"
	onclick={onClose}
	role="dialog"
	tabindex="-1"
	aria-modal="true"
>
	<button 
		class="close-button"
		onclick={onClose}
		aria-label="Close"
	>
		<X size={40} />
	</button>
	
	{#if images.length > 1}
		<button class="nav-button prev" onclick={prev} aria-label="Previous image">
			<ChevronLeft size={40} />
		</button>
		<button class="nav-button next" onclick={next} aria-label="Next image">
			<ChevronRight size={40} />
		</button>
	{/if}

	<img 
		src={images[currentIndex]} 
		alt="Full view" 
		class="full-image"
		onclick={(e) => e.stopPropagation()} 
	/>

	{#if images.length > 1}
		<div class="dots">
			{#each images as _, i}
				<button 
					class="dot {i === currentIndex ? 'active' : ''}"
					onclick={(e) => { e.stopPropagation(); currentIndex = i; }}
					aria-label="Go to image {i + 1}"
				></button>
			{/each}
		</div>
	{/if}
</div>

<style>
	.image-viewer-overlay {
		position: fixed;
		top: 0;
		left: 0;
		width: 100vw;
		height: 100vh;
		z-index: 99999;
		background-color: rgba(0, 0, 0, 0.95);
		display: flex;
		align-items: center;
		justify-content: center;
		padding: 1rem;
		backdrop-filter: blur(4px);
		animation: fadeIn 0.2s ease-out forwards;
	}

	.close-button {
		position: absolute;
		top: 1.5rem;
		right: 1.5rem;
		color: rgba(255, 255, 255, 0.7);
		background: none;
		border: none;
		cursor: pointer;
		transition: color 0.2s;
		z-index: 100000;
	}

	.close-button:hover {
		color: #C5A059;
	}

	.nav-button {
		position: absolute;
		top: 50%;
		transform: translateY(-50%);
		background: rgba(0, 0, 0, 0.5);
		color: white;
		border: none;
		padding: 1rem;
		cursor: pointer;
		z-index: 100000;
		border-radius: 50%;
		display: flex;
		align-items: center;
		justify-content: center;
		transition: background 0.2s;
	}
	.nav-button:hover {
		background: rgba(197, 160, 89, 0.8);
	}
	.prev { left: 2rem; }
	.next { right: 2rem; }

	.dots {
		position: absolute;
		bottom: 2rem;
		left: 50%;
		transform: translateX(-50%);
		display: flex;
		gap: 0.5rem;
		z-index: 100000;
	}
	.dot {
		width: 10px;
		height: 10px;
		border-radius: 50%;
		background: rgba(255, 255, 255, 0.3);
		border: none;
		cursor: pointer;
		padding: 0;
		transition: all 0.2s;
	}
	.dot.active {
		background: #C5A059;
		transform: scale(1.2);
	}

	.full-image {
		max-width: 100%;
		max-height: 90vh;
		object-fit: contain;
		border-radius: 4px;
		box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
	}

	@keyframes fadeIn {
		from { opacity: 0; }
		to { opacity: 1; }
	}
</style>
