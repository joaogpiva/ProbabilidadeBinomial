<script lang="ts">
    import { display } from 'mathlifier';

    let p: number, n: number, x: number, resultIndividual: number = 0, resultAcumulada: number = 0;
    $: eq = display("P(x) = {" + (n ? n : 0) +  "\\choose " + (x ? x : 0) + "} \\cdot " 
                    + (p ? p : 0) + "^{" + (x ? x : 0) + "} \\cdot " 
                    + (p ? (1-p) : 1) + "^{" + (x && n ? (n - x) : 0) + "}");
    function handleClick () {
        
	}
</script>

<div class="d-flex flex-column align-items-center justify-content-center p-2">
    <h1>Calculadora de Probabilidade Binomial</h1>

    <input bind:value={p} placeholder="Digite o valor de p" />
    <input bind:value={n} placeholder="Digite o valor de n" />
    <input bind:value={x} placeholder="Digite o valor de x" />

    <p>{@html eq}</p>
    
    <button on:click={handleClick}>Calcular</button>
    
    <h2>Resultado da probabilidade individual: { resultIndividual }</h2>
    <h2>Resultado da probabilidade acumulada: { resultAcumulada }</h2>
</div>