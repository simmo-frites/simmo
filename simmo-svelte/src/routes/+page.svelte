<script lang="ts">
  import type { ActionData } from './$types';

  export let form: ActionData;

  let amount = form?.body?.settings.amount || 100000;
  let duration = form?.body?.settings.duration || 20;
  let rate = form?.body?.settings.rate || 3;
  let income = form?.body?.settings.income || 2000;
</script>

<h1>Simmo 🍟</h1>

<form method="post">
  <label>
    Montant emprunté
    <input type="number" name="amount" min="0" step="1000" value={amount} required />
  </label>

  <label>
    Durée du pret en années
    <input type="number" name="duration" min="1" max="30" step="1" value={duration} required />
  </label>

  <label>
    Taux annuel
    <input type="number" name="rate" min="0" max="100" step="0.05" value={rate} required />
  </label>

  <label>
    Revenus mensuels nets avant impots
    <input type="number" name="income" min="0" step="50" value={income} required />
  </label>

  <button>Calculer</button>
</form>

{#if form?.body}
  <section class="results">
    <div class="results-items">
      <div>
        <h2>Taux d'endettement</h2>
        <p>{form.body.results.debtLoanRatio.toFixed(1)} %</p>
      </div>
      <div>
        <h2>Mensualités</h2>
        <p>{form.body.results.monthlyLoanCost.toFixed(0)} €</p>
      </div>
      <div>
        <h2>Total des intérets</h2>
        <p>
          {form.body.results.totalLoanCost.toFixed(0)} €
        </p>
      </div>
    </div>
    <div>
      <a
        class="advanced"
        hidden={true}
        href={`/advanced?amount=${amount}&duration=${duration}&rate=${rate}&income=${income}`}
        >Mode avancé 🛠️</a
      >
    </div>
  </section>
{/if}

<style>
  * {
    box-sizing: border-box;
    font-family: 'Courier New', Courier, monospace;
  }

  h1 {
    text-align: center;
  }

  input {
    display: block;
    margin: 0.5rem 0;
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 0.25rem;
    padding: 0.5rem;
    width: 100%;
  }

  form {
    max-width: 30rem;
    margin: 2rem auto;
    padding: 0 2rem;
  }

  button {
    display: block;
    margin: 2rem auto;
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 0.25rem;
    padding: 0.5rem;
    width: 75%;
    background-color: #ccc;
    cursor: pointer;
    font-size: 1rem;
    font-weight: bold;
  }

  section {
    display: flex;
    justify-content: space-around;
    margin-top: 2rem;
  }

  section > div {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
  }

  section > div > div > p {
    font-size: 2rem;
    font-weight: bold;
    text-align: center;
  }

  .results {
    margin: 2rem auto;
    flex-direction: column;
  }

  .results-items {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    max-width: 900px;
    margin: 0 auto;
  }

  .results-items > div {
    padding: 0 2rem;
  }

  a {
    display: block;
    margin: 2rem auto;
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 0.25rem;
    padding: 0.5rem;
    width: min(75%, 15rem);
    background-color: #c7c689;
    cursor: pointer;
    font-size: 1rem;
    font-weight: bold;
    text-align: center;
    text-decoration: none;
    color: black;
  }
</style>
