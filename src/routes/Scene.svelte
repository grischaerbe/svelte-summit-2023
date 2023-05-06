<script lang="ts">
	import { T, useFrame } from '@threlte/core'
	import {
		Environment,
		Text,
		interactivity
	} from '@threlte/extras'
	import Ticket from './Ticket.svelte'
	import {
		DEG2RAD,
		RAD2DEG
	} from 'three/src/math/MathUtils'
	import { spring } from 'svelte/motion'

	let rotationY = 0

	useFrame((_, delta) => {
		rotationY += 0.1 * delta
		if (rotationY * RAD2DEG > 90) {
			rotationY -= 180 * DEG2RAD
		}
	})

	interactivity()

	const scale = spring(1)
</script>

<T.PerspectiveCamera
	makeDefault
	fov={10}
	position={[0, 0, 40]}
/>

<Environment files="/oil-on-water.png" />

<T.Group
	rotation.y={rotationY}
	on:pointerenter={() => {
		scale.set(1.1)
	}}
	on:pointerleave={() => {
		scale.set(1)
	}}
	scale={$scale}
>
	<Text
		text="Max Mustermann"
		font="/Flama.otf"
		fontSize={0.25}
		position={[-0.8, -0.35, 0.04]}
		maxWidth={1.5}
	>
		<T.MeshStandardMaterial envMapIntensity={11} />
	</Text>

	<Text
		text="NO. 12345"
		font="/Flama.otf"
		fontSize={0.25}
		position={[0, 1.88, 0.04]}
		anchorX="50%"
		anchorY="50%"
	>
		<T.MeshStandardMaterial
			envMapIntensity={11}
			color="black"
			roughness={0}
		/>
	</Text>

	<Ticket />
</T.Group>
