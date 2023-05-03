<script lang="ts">
    import { math, display } from 'mathlifier';

    let p: number, n: number, x: number, resultIndividual = 0, resultAcumulado = 0;
    $: eq = display("P(x) = {" + (n ? n : 0) +  "\\choose " + (x ? x : 0) + "} \\cdot " 
                    + (p ? p : 0) + "^{" + (x ? x : 0) + "} \\cdot " 
                    + (p && p != 0 ? (1-p).toFixed(p.toString().split(".")[1].length) : 1) + "^{" + (x && n ? (n - x) : 0) + "}");

    $: exprProbabilidadeIndividual = math("P(x = " + (x ? x : 0) + ")");
    $: exprProbabilidadeAcumulada = math("P(x \\le " + (x ? x : 0) + ")");
       

    function handleClick() {
        if (!validateInputs(p, n, x)){
            let resString = "";

            if(p > 1 || p < 0)
                resString += "O valor de p deve ser entre 0 e 1, separando as casas decimais com ponto (por exemplo, 0.45)\n"

            if(x > n)
                resString += "O valor de x não pode ser maior que o valor de n\n";

            let invalidInputs : string[] = [];
            if (!p || p < 0) invalidInputs.push("p");
            if (!n || n < 0) invalidInputs.push("n");
            if (!x || x < 0) invalidInputs.push("x");
            if(invalidInputs.length != 0)
                resString += "Entradas inválidas: " + invalidInputs.join(", ");
            
            alert(resString);

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
        if (p > 1 || p < 0)
            return false
        if (!n || !x || !p) 
            return false;
        if (n < 0 || x < 0 || p < 0)
            return false;
        if (x > n) 
            return false;
        return true;
    }

    function fatorial(numero: number): number {
        if (numero < 0)
            return 1;
        return numero === 0 ? 1 : numero * fatorial(numero - 1);
    }
</script>

<div class="d-flex flex-column align-items-center justify-content-center min-vh-100 container-geral" >
    <div class="p-3">
        <h1>Calculadora de Probabilidade Binomial</h1>
    </div>

    <div class="d-flex flex-column align-items-center justify-content-center p-3">
        <form>
            <div class="mb-2">
                <input class="form-control" type="number" bind:value={p} placeholder="Digite o valor de p" />
            </div>
            <div class="mb-2">
                <input class="form-control" type="number" bind:value={n} placeholder="Digite o valor de n" />
            </div>
            <div class="mb-2">
                <input class="form-control" type="number" bind:value={x} placeholder="Digite o valor de x" />
            </div>
        </form> 

        <p>{@html eq}</p>
        <button class="btn btn-primary btn-calcular" on:click={handleClick}>Calcular</button>
    </div>

    <div class="p-3 d-flex flex-column align-items-center justify-content-center">
        <div class="resultado">
            <h2>Resultado da probabilidade individual ({@html exprProbabilidadeIndividual}): { resultIndividual.toFixed(4) }</h2>
        </div>
        <div class="resultado">
            <h2>Resultado da probabilidade acumulada ({@html exprProbabilidadeAcumulada}): { resultAcumulado.toFixed(4) }</h2>
        </div>
    </div>
</div>

<style>
.container-geral{
    background-color: rgb(162, 255, 162);
}

.btn-calcular{
    color: rgb(162, 255, 162);
    background-color: rgb(0,111,60);
    border-color: #005930;
}

.resultado{
    display: flex;
    background-color: rgb(0,111,60);
    border: 3px;
    border-color: #005930;
    color: rgb(162, 255, 162);
    border-radius: 5px;
    padding: 0.7rem;
    margin: 0.3rem;
    width: 100%;
    justify-content: center;
}
</style>
