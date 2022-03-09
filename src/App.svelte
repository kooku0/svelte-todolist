<script lang="ts">
  let id = 0;
  let value: string;
  let items = [];

  function addItem() {
    items = [...items, { id, value, complete: false }];
    value = "";
    id += 1;
  }
  function deleteItem(id) {
    items = items.filter((item) => item.id !== id);
  }
  function completeItem(id) {
    items = items.map((item) => {
      if (item.id === id) {
        return {
          ...item,
          complete: !item.complete,
        };
      }

      return {
        ...item,
      };
    });
  }
</script>

<main>
  <h1>TodoList</h1>
  <input bind:value />
  <button on:click={addItem}>click</button>
  {#each items as { value, complete, id } (id)}
    <div>
      <span>{value}</span>
      <span>
        <button disabled={complete} on:click={() => completeItem(id)}>
          complete
        </button>
        <button on:click={() => deleteItem(id)}>delete</button>
      </span>
    </div>
  {/each}
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
