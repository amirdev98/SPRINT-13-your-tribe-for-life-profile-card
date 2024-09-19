<script>
	/** @type {import("@prismicio/client").Content.PageContentSlice} */
	export let slice;
</script>

<section data-slice-type={slice.slice_type} data-slice-variation={slice.variation}>
	<h1>{slice.primary.textfield}</h1>
</section>

<style>
	h1 {
		color: #333;
		font-size: 2rem;
		text-align: center;
		margin: 4rem;
			font-family: 'Alegreya', serif;
	}
</style>
