<script lang="ts">
  import PeriodicTable from "../components/PeriodicTable/PeriodicTable.svelte";
  import {
    colors,
    type PeriodicElement,
  } from "../components/PeriodicTable/elements";

  let selected = $state<PeriodicElement | null>(null);
  let mode: "symbol" | "name" = $state("symbol");

  function onClick(element: PeriodicElement | null) {
    selected = element;
  }
</script>

<svelte:head>
  <title>Periodic Table</title>
</svelte:head>

<div class="p-4">
  <h1 class="mb-6 text-center text-2xl font-bold sm:text-3xl">
    Periodic Table Quiz
  </h1>
  <div class="mb-4 flex justify-center">
    <button
      class="rounded border px-3 py-1 text-sm font-medium transition hover:bg-gray-100"
      onclick={() => (mode = mode === "symbol" ? "name" : "symbol")}
    >
      Show: {mode === "symbol" ? "Symbol" : "Name"}
    </button>
  </div>
  <PeriodicTable {onClick} {mode} />
  {#if selected}
    <div class="mt-4 flex justify-center">
      <div class="rounded-lg border border-gray-300 bg-white p-4 shadow-sm">
        <div class="flex items-center gap-3">
          <div
            class="grid h-16 w-16 place-items-center rounded border-2 border-gray-400"
            class:list={colors[selected.category] ??
              "bg-gray-300 text-gray-900"}
          >
            <span class="text-2xl font-bold">{selected.symbol}</span>
          </div>
          <div>
            <h3 class="text-lg font-semibold">{selected.name}</h3>
            <!-- <p class="text-sm opacity-50">{selected.category}</p> -->
          </div>
        </div>
      </div>
    </div>
  {/if}
</div>
