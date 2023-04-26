<script lang="ts">
    let p: number, n: number, x: number, resultIndividual: number = 0, resultAcumulado: number = 0;

    function handleClick() {
        if (!validateInputs(p, n, x)){
            //TODO
            return;
        }        

        let nFatorial = fatorial(n);
        let xFatorial = fatorial(x);
        let nSubxFatorial = fatorial(n-x);

        resultIndividual = (nFatorial / (xFatorial * nSubxFatorial)) * (p ** x) * ((1-p) ** (n - x));
        resultAcumulado = resultIndividual;

        for (let index = 0; index <= x-1; index++) {
            let indexFatorial = fatorial(index);
            let nSubIndexFatorial = fatorial(n-index);
            resultAcumulado += (nFatorial / (indexFatorial * nSubIndexFatorial)) * (p ** index) * ((1-p) ** (n - index));     
        }
	}

    function validateInputs(p: number, n: number, x: number): boolean {
        if (!n || !x || !p) {
            return false;
        }
        if (x > n) {
            return false;
        }
        return true;
    }

    function fatorial(numero: number): number {
        if (numero < 0)
            return 1;
        return numero === 0 ? 1 : numero * fatorial(numero - 1);
    };
</script>

<h1>Calculadora de Probabilidade Binomial</h1>

<input bind:value={p} type="number" placeholder="Digite o valor de p" />
<input bind:value={n} type="number" placeholder="Digite o valor de n" />
<input bind:value={x} type="number" placeholder="Digite o valor de x" />

<button on:click={handleClick}>Calcular</button>

<h3>Resultado individual: {resultIndividual}</h3>
<h3>Resultado acumulado: {resultAcumulado}</h3>