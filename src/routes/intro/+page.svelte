<script lang="ts">
	import { Canvas } from '@threlte/core'
	import Scene from './Scene.svelte'
	import Export from '../Export.svelte'
</script>

<div class="w-screen h-screen bg-black">
	<div class="absolute top-0 w-full pointer-events-none">
		<h1
			class="text-center my-6 text-white w-full font-bold text-6xl"
		>
			THRELTE CONF 2023
		</h1>
	</div>

	<div class="absolute w-full h-full top-0 left-0">
		<!-- INSERT FANCY TICKET GRAPHICS HERE -->
		<Canvas>
			<Scene />
		</Canvas>
	</div>

	<div
		class="absolute left-6 bottom-6 pointer-events-none rounded-xl border border-gray-700 px-6 py-6 text-white bg-gradient-to-br from-blue-950 to-fuchsia-950"
	>
		<h1 class="font-bold text-xl mb-4">Your Ticket</h1>
		<div>
			Grischa Erbe<br />
			Ticket No. 12345
		</div>
	</div>

	<div
		class="absolute bottom-6 right-6 [&_svg]:!fill-white [&_svg]:w-10"
	>
		<Export />
	</div>
</div>
