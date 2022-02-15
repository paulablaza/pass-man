<script>
  import '../node_modules/bulma/css/bulma.min.css';

  import Clipboard from 'svelte-clipboard';
  import { generatePassword } from 'passWhip';

  let password = generatePassword({
    numbers: true,
  });

  // 'uEyMTw32v9'
  console.log(password);

  let input;
  let length = 15;
  let lowercase = true;
  let uppercase = true;
  let numbers = true;
  let symbols = true;

  const generate = () => {
    password = generatePassword({
      length: length,
      lowercase: lowercase,
      uppercase: uppercase,
      numbers: numbers,
      symbols: symbols,
    });
    input.value = password;
  };
</script>

<div class="card">
  <header class="card-header">
    <input
      bind:this={input}
      class="input"
      type="text"
      placeholder="Password Generated"
      autofocus
    />
    <Clipboard
      text={password}
      let:copy
      on:copy={() => {
        input.select();
        console.log('Has Copied');
      }}
    >
      <button class="button is-primary" on:click={copy}>Copy</button>
    </Clipboard>
  </header>

  <div class="card-content">
    <div class="is-flex is-align-items-center	mx-1 mt-1">
      <span class="p-0">Password Length</span>
      <input
        class="input ml-auto is-small is-primary"
        type="number"
        bind:value={length}
        max="25"
      />
    </div>
    <div class="is-flex is-align-items-center	mx-1 mt-2">
      <span class=" p-0">Uppercase Letters</span>
      <input class="ml-auto" type="checkbox" bind:checked={uppercase} />
    </div>
    <div class="is-flex is-align-items-center	mx-1 mt-2">
      <span class="  p-0">Lowercase Letters</span>
      <input class="ml-auto" type="checkbox" bind:checked={lowercase} />
    </div>
    <div class="is-flex is-align-items-center	mx-1 mt-2">
      <span class="p-0">Numbers</span>
      <input class="ml-auto" type="checkbox" bind:checked={numbers} />
    </div>
    <div class="is-flex is-align-items-center	mx-1 mt-2 mb-1">
      <span class="  p-0">Symbols</span>
      <input class="ml-auto" type="checkbox" bind:checked={symbols} />
    </div>
  </div>

  <button on:click={generate} class="generate-button button is-primary is-full"
    >Generate</button
  >
</div>

<style type="text/scss">
  input:focus {
    border-color: inherit;
    -webkit-box-shadow: none;
    box-shadow: none;
  }

  input {
    width: 50px;
  }

  :global(body) {
    background-color: rgb(27, 27, 27);
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .card {
    width: 40rem;
    max-width: 400px;

    header {
      display: flex;
      align-items: center;
      justify-content: center;

      input {
        width: 90%;
        height: 90%;
        border: none;
        background: none;
      }
    }

    .generate-button {
      width: 100%;
    }
  }
</style>
