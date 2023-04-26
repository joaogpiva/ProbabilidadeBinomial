<script lang="ts">
    let p: number, n: number, x: number, resultIndividual: number, resultAcumulado: number;

    function handleClick() {
        let nFatorial = fatorial(n);
        let xFatorial = fatorial(x);
        let nSubxFatorial = fatorial(n-x);
       
        resultIndividual = nFatorial / xFatorial * nSubxFatorial * (p ** x) * ((1-p) ** (n - x));
	}

    function fatorial(numero: number): number {
        if (numero < 0) {
            return 1;
        }
        return numero === 0 ? 1 : numero * fatorial(numero - 1);
    };
</script>

<h1>Calculadora de Probabilidade Binomial</h1>

<input bind:value={p} placeholder="Digite o valor de p" />
<input bind:value={n} placeholder="Digite o valor de n" />
<input bind:value={x} placeholder="Digite o valor de x" />

<button on:click={handleClick}>Calcular</button>

<h3>Resultado individual: {resultIndividual}</h3>
<h3>Resultado acumulado: {resultAcumulado}</h3>