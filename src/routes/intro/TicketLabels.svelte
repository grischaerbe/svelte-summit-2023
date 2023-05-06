<script lang="ts">
	import { T } from '@threlte/core'
	import { Text } from '@threlte/extras'
	import { DEG2RAD } from 'three/src/math/MathUtils'
</script>

<T.Group {...$$restProps}>
	<Text
		position={[-0.8, 0.04, 0.4]}
		rotation.x={-90 * DEG2RAD}
		text="Grischa Erbe"
		fontSize={0.2}
		maxWidth={1.5}
		font="/Flama.otf"
	>
		<T.MeshStandardMaterial envMapIntensity={10} />
	</Text>

	<Text
		position={[0, 0.04, -1.9]}
		rotation.x={-90 * DEG2RAD}
		text="NO. 12345"
		fontSize={0.2}
		maxWidth={1.8}
		textAlign="center"
		anchorX="50%"
		anchorY="50%"
		let:ref
		font="/Flama.otf"
	>
		<T.MeshStandardMaterial
			roughness={0}
			color="black"
			envMapIntensity={10}
		/>
	</Text>

	<Text
		position={[0, 0.04, 1.9]}
		rotation.x={-90 * DEG2RAD}
		text="23.11.2023"
		fontSize={0.2}
		maxWidth={1.8}
		textAlign="center"
		anchorX="50%"
		anchorY="50%"
		let:ref
		font="/Flama.otf"
	>
		<T.MeshStandardMaterial
			roughness={0}
			color="black"
			envMapIntensity={10}
		/>
	</Text>
</T.Group>
