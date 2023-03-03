<script>
  import Web3 from 'web3';
  import Contract from './Contract.json';
  
  const web3 = new Web3(Web3.givenProvider);
  const contract = new web3.eth.Contract(Contract.abi, Contract.address);
  
  let message = '';
  async function setMessage() {
    await contract.methods.setMessage(message).send({ from: web3.eth.accounts[0] });
  }
  
  async function getMessage() {
    const result = await contract.methods.getMessage().call();
    message = result;
  }
  
  getMessage();
</script>

<main>
  <h1>My dApp</h1>
  <form on:submit|preventDefault="{setMessage}">
    <label>
      Message:
      <input bind:value="{message}">
    </label>
    <button type="submit">Submit</button>
  </form>
  <p>The current message is: {message}</p>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
