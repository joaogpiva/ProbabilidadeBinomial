<script lang="ts">
    let p: number, n: number, x: number;
    function handleClick () {
        
	}
</script>

<h1>Calculadora de Probabilidade Binomial</h1>

<input bind:value={p} placeholder="Digite o valor de p" />
<input bind:value={n} placeholder="Digite o valor de n" />
<input bind:value={x} placeholder="Digite o valor de x" />

<button on:click={handleClick}>Calcular</button>