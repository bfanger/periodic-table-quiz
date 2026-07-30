<script lang="ts">
  import { resolve } from "$app/paths";
  import PeriodicTable from "../components/PeriodicTable/PeriodicTable.svelte";
  import ElementSummary from "../components/ElementSummary.svelte";
  import Toggle from "../components/Toggle.svelte";
  import type { PeriodicElement } from "../elements";

  let selected = $state<PeriodicElement>();
  let mode: "symbol" | "name" = $state("symbol");

  function onClick(element: PeriodicElement) {
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
  <div class="mb-4 flex justify-center gap-4">
    <a
      href={resolve("/quiz/name")}
      class="rounded border px-3 py-1 text-sm font-medium transition hover:bg-gray-100"
    >
      Guess the name
    </a>
    <a
      href={resolve("/quiz/symbol")}
      class="rounded border px-3 py-1 text-sm font-medium transition hover:bg-gray-100"
    >
      Guess the symbol
    </a>
  </div>
  <div class="mb-4 flex justify-center">
    <Toggle
      left={{ label: "Symbol", value: "symbol" }}
      right={{ label: "Name", value: "name" }}
      bind:value={mode}
    />
  </div>
  <PeriodicTable {onClick} {mode} />
  {#if selected}
    <ElementSummary element={selected} />
  {/if}
</div>
