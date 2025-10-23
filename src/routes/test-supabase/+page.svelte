<script lang="ts">
	import { supabase } from '$lib/supabaseClient';
	let connection: string | null = null;

	const testConnection = async () => {
		const { error } = await supabase.from('pg_tables').select('*').limit(1);
		connection = error ? 'Falha na conexao com Supabase' : 'Conexao com Supabase bem-sucedida';
	};

	testConnection();
</script>

<section class="flex flex-col items-center justify-center min-h-screen space-y-6">
	<h1 class="text-2xl font-bold">Teste de Conexao Supabase</h1>
	<p>{connection}</p>
</section>
