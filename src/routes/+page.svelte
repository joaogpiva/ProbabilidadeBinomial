<script lang="ts">
    import { math, display } from 'mathlifier';

    let p: number, n: number, x: number, resultIndividual: number = 0, resultAcumulada: number = 0;
    $: eq = display("P(x) = {" + (n ? n : 0) +  "\\choose " + (x ? x : 0) + "} \\cdot " 
                    + (p ? p : 0) + "^{" + (x ? x : 0) + "} \\cdot " 
                    + (p && p != 0 ? (1-p).toFixed(p.toString().split(".")[1].length) : 1) + "^{" + (x && n ? (n - x) : 0) + "}");

    $: exprProbabilidadeIndividual = math("P(x = " + (x ? x : 0) + ")");
    $: exprProbabilidadeAcumulada = math("P(x \\le " + (x ? x : 0) + ")");

    function handleClick () {
        
	}
</script>

<div class="d-flex flex-column align-items-center justify-content-center min-vh-100 container-geral" >
    <div class="p-3">
        <h1>Calculadora de Probabilidade Binomial</h1>
    </div>

    <div class="d-flex flex-column align-items-center justify-content-center p-3">
        <form>
            <div class="mb-2">
                <input class="form-control" bind:value={p} placeholder="Digite o valor de p" />
            </div>
            <div class="mb-2">
                <input class="form-control" bind:value={n} placeholder="Digite o valor de n" />
            </div>
            <div class="mb-2">
                <input class="form-control" bind:value={x} placeholder="Digite o valor de x" />
            </div>
        </form> 

        <p>{@html eq}</p>
        <button class="btn btn-primary btn-calcular" on:click={handleClick}>Calcular</button>
    </div>

    <div class="p-3 d-flex flex-column align-items-center justify-content-center">
        <h2>Resultado da probabilidade individual ({@html exprProbabilidadeIndividual}): { resultIndividual }</h2>
        <h2>Resultado da probabilidade acumulada ({@html exprProbabilidadeAcumulada}): { resultAcumulada }</h2>
    </div>
</div>

<style>
.container-geral{
    background-color: rgb(162, 255, 162);
}

.btn-calcular{
    background-color: rgb(0,111,60);
    border-color: #005930;
}
</style>