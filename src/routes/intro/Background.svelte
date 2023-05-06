<script lang="ts">
	import { T } from '@threlte/core'
	import { createTransition, transitions, useTexture } from '@threlte/extras'
	import { DoubleSide, Material } from 'three'

	transitions()

	const fade = (opacity: number) =>
		createTransition<Material>((ref) => {
			ref.transparent = true
			return {
				tick: (t: number) => {
					ref.opacity = t * opacity
				},
				delay: 1e3,
				duration: 2e3
			}
		})
</script>

{#await useTexture('/background.png') then texture}
	<T.Mesh {...$$restProps}>
		<T.PlaneGeometry />

		<T.MeshBasicMaterial
			transition={fade(0.4)}
			map={texture}
			transparent
			side={DoubleSide}
			toneMapped={false}
		/>

		<slot />
	</T.Mesh>
{/await}
