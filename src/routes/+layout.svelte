<script lang="ts">
	import { onMount } from "svelte"
	import { invalidate } from "$app/navigation"
	export let data
	$: ({ supabase } = data)

	onMount(() => {
		const { data: { subscription } } = supabase.auth.onAuthStateChange(() => {
			invalidate('supabase:auth')
		})

		return () => subscription.unsubscribe()
	})
</script>


<a href="/login">Login</a>
<slot />