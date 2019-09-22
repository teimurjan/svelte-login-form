<script>
  import { onMount, setContext } from "svelte";

  import {
    key as userContextKey,
    initialValue as userContextInitialValue
  } from "./userContext";

  import LoginForm from "./LoginForm.svelte";

  onMount(() => {
    setContext(userContextKey, userContextInitialValue);
  });

  const submit = ({ email, password }) =>
    new Promise((resolve, reject) => {
      setTimeout(() => {
        setContext(userContextKey, {
          name: "Foo",
          lastName: "Bar",
          email: "foo@bar.com"
        });
        resolve();
      }, 1000);
    });
</script>

<style>
  section {
    height: 100vh;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    background: linear-gradient(to right, #cd76e2, #e358ab);
  }
</style>

<section>
  <LoginForm {submit} />
</section>
