<script>
  import { Input, Label, Tabs, TabItem, Helper, Toggle } from "flowbite-svelte";
  import Gerbang from "../vendor/kunci/src/Gerbang.svelte";

  let inputanBaru = "";
  //   data[] -> todo, isDone
  let data = [];
  if (localStorage.data) {
    data = JSON.parse(localStorage.data);
  }
  function onAdd() {
    data = [
      ...data,
      {
        todo: inputanBaru,
        isDone: false,
      },
    ];
    localStorage.data = JSON.stringify(data);
    inputanBaru = "";
  }
</script>

<Gerbang namaAplikasi="TODO">
  {#if data.length > 0}
    <Tabs
      contentClass="bg-white"
      class="sticky top-0 left-0 bg-white z-[10]"
      style="underline"
    >
      <TabItem open title="❌">
        <div class="mb-[50px] p-5">
          {#each data as item}
            {#if item.isDone == false}
              <Toggle
                class="text-lg mb-5 last:mb-0"
                on:change={() => {
                  item.isDone = !item.isDone;
                  localStorage.data = JSON.stringify(data);
                }}
                checked={item.isDone}>{item.todo}</Toggle
              >
            {/if}
          {/each}
        </div>
      </TabItem>
      <TabItem title="✔️">
        <div class="mb-[50px] p-5">
          {#each data as item}
            {#if item.isDone == true}
              <Toggle
                class="text-lg mb-5 last:mb-0"
                on:change={() => {
                  item.isDone = !item.isDone;
                  localStorage.data = JSON.stringify(data);
                }}
                checked={item.isDone}>{item.todo}</Toggle
              >
            {/if}
          {/each}
        </div>
      </TabItem>
    </Tabs>
  {/if}
  <form on:submit|preventDefault={onAdd} class="fixed w-full bottom-0 left-0">
    <Input
      type="text"
      class="rounded-none"
      id="first_name"
      placeholder="New TODO"
      required
      bind:value={inputanBaru}
    />
  </form>
</Gerbang>
