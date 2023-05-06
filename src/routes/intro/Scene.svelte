<script lang="ts">
	import { T, useFrame } from '@threlte/core'
	import {
		Environment,
		interactivity
	} from '@threlte/extras'
	import { spring } from 'svelte/motion'
	import { DEG2RAD } from 'three/src/math/MathUtils'
	import Ticket from '../Ticket.svelte'
	import Background from './Background.svelte'
	import TicketLabels from './TicketLabels.svelte'

	interactivity()

	let shouldRotate = true

	const rotation = spring(0, {
		precision: 0.00001
	})
	useFrame(() => {
		if (!shouldRotate) return

		const newRotation = $rotation + 0.02
		if (newRotation > 180 * DEG2RAD) {
			rotation.set(newRotation - 180 * DEG2RAD, {
				hard: true
			})
		} else {
			rotation.set(newRotation)
		}
	})

	const parentRotation = spring(
		[-25 * DEG2RAD, 21 * DEG2RAD, -22 * DEG2RAD] as [
			number,
			number,
			number
		],
		{
			precision: 0.00001
		}
	)

	const scale = spring(1, {
		precision: 0.00001
	})
</script>

<Environment files="/oil-on-water.png" />

<T.PerspectiveCamera
	position={[0, 0, 40]}
	makeDefault
	fov={10}
	on:create={({ ref }) => {
		ref.lookAt(0, 0, 0)
	}}
/>

<T.Group rotation={$parentRotation} scale={$scale}>
	<Ticket
		rotation={[0, $rotation, 0]}
		on:pointerenter={() => {
			shouldRotate = false
			if ($rotation > 60 * DEG2RAD) {
				rotation.set(180 * DEG2RAD)
			} else {
				rotation.set(0)
			}
			parentRotation.set([0, 0, 0])
			scale.set(1.1)
		}}
		on:pointerleave={() => {
			shouldRotate = true
			parentRotation.set([
				-25 * DEG2RAD,
				21 * DEG2RAD,
				-22 * DEG2RAD
			])
			scale.set(1)
		}}
	>
		<TicketLabels rotation.x={90 * DEG2RAD} />

		<T.Group
			rotation.z={180 * DEG2RAD}
			rotation.x={90 * DEG2RAD}
		>
			<TicketLabels />
		</T.Group>
	</Ticket>
</T.Group>

<Background position.z={-20} scale={9} />
