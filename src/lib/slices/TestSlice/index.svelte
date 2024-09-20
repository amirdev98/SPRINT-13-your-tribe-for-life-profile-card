<script>
	/** @type {import("@prismicio/client").Content.TestSliceSlice} */
	import { PrismicImage } from '@prismicio/svelte';

	export let slice;
</script>

<section class="img-wrapper" data-slice-type={slice.slice_type} data-slice-variation={slice.variation}>
	{#each slice.items as item}
		<figure class="PrismicImage">
			<PrismicImage field={item.imagefield}  />
		</figure>
	{/each}
</section>

<style>


    section[data-slice-type] {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 20px;
        padding: 20px;
        background-color: #002b5b;
        border-radius: 2rem;
    }

    .PrismicImage {
        width: 200px; /* Adjust this if you want a different size */
        /*height: auto;*/
        height: 300px;
        overflow: hidden;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        transition: transform 0.2s;
        border-radius: 1rem; /* Apply border-radius here */
        margin: 0 !important;

    }

    .PrismicImage:hover {
        transform: scale(1.05);
    }

    .PrismicImage img {
        width: 100%;
        height: 100%;
        object-fit: cover;
        border-radius: 1rem; /* Ensure the image itself has the border-radius */
    }

    .PrismicImage .caption {
        background-color: rgba(0, 0, 0, 0.7);
        color: #fff;
        padding: 5px;
        text-align: center;
        font-size: 14px;
        position: absolute;
        bottom: 0;
        left: 0;
        width: 100%;
        transition: opacity 0.2s;
        opacity: 0;
    }

    .PrismicImage:hover .caption {
        opacity: 1;
    }
</style>