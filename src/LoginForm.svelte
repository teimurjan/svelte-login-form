<script>
  let email = "";
  let password = "";

  let isLoading = false;

  let isSuccess = false;

  export let submit;

  let errors = {};

  const handleSubmit = () => {
    errors = {};

    if (email.length === 0) {
      errors.email = "Field should not be empty";
    }
    if (password.length === 0) {
      errors.password = "Field should not be empty";
    }

    if (Object.keys(errors).length === 0) {
      isLoading = true;
      submit({ email, password })
        .then(() => {
          isSuccess = true;
          isLoading = false;
        })
        .catch(err => {
          errors.server = err;
          isLoading = false;
        });
    }
  };
</script>

<style>
  form {
    background: #fff;
    padding: 50px;
    width: 250px;
    height: 400px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    box-shadow: 0px 20px 14px 8px rgba(0, 0, 0, 0.58);
  }

  label {
    margin: 10px 0;
    align-self: flex-start;
    font-weight: 500;
  }

  input {
    border: none;
    border-bottom: 1px solid #ccc;
    margin-bottom: 20px;
    transition: all 300ms ease-in-out;
    width: 100%;
  }

  input:focus {
    outline: 0;
    border-bottom: 1px solid #666;
  }

  button {
    margin-top: 20px;
    background: black;
    color: white;
    padding: 10px 0;
    width: 200px;
    border-radius: 25px;
    text-transform: uppercase;
    font-weight: bold;
    cursor: pointer;
    transition: all 300ms ease-in-out;
  }

  button:hover {
    transform: translateY(-2.5px);
    box-shadow: 0px 1px 10px 0px rgba(0, 0, 0, 0.58);
  }

  h1 {
    margin: 10px 20px 30px 20px;
    font-size: 40px;
  }

  .errors {
    list-style-type: none;
    padding: 10px;
    margin: 0;
    border: 2px solid #be6283;
    color: #be6283;
    background: rgba(190, 98, 131, 0.3);
  }

  .success {
    font-size: 24px;
    text-align: center;
  }
</style>

<form on:submit|preventDefault={handleSubmit}>
  {#if isSuccess}
    <div class="success">
      🔓
      <br />
      You've been successfully logged in.
    </div>
  {:else}
    <h1>👤</h1>

    <label>Email</label>
    <input name="email" placeholder="name@example.com" bind:value={email} />

    <label>Password</label>
    <input name="password" type="password" bind:value={password} />

    <button type="submit">
      {#if isLoading}Logging in...{:else}Log in 🔒{/if}
    </button>

    {#if Object.keys(errors).length > 0}
      <ul class="errors">
        {#each Object.keys(errors) as field}
          <li>{field}: {errors[field]}</li>
        {/each}
      </ul>
    {/if}
  {/if}
</form>
