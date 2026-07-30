<script lang="ts">
  import ElementSummary from "./ElementSummary.svelte";
  import PeriodicTable from "./PeriodicTable/PeriodicTable.svelte";
  import Score from "./Score.svelte";
  import { elements, type PeriodicElement } from "../elements";
  import { onMount } from "svelte";
  import { Confetti } from "svelte-confetti";
  import { resolve } from "$app/paths";

  let { mode }: { mode: "symbol" | "name" } = $props();

  let current = $state<PeriodicElement>();
  let selected = $state<PeriodicElement>();
  let score = $state(0);

  let result = $derived(
    selected === undefined
      ? undefined
      : selected.symbol === current?.symbol
        ? "correct"
        : "wrong",
  );

  function getRandom(): PeriodicElement {
    return elements[Math.floor(Math.random() * elements.length)]!;
  }
  onMount(() => {
    current = getRandom();
  });

  function onClick(element: PeriodicElement) {
    if (selected) {
      return;
    }
    selected = element;

    if (selected.symbol === current?.symbol) {
      score += 100;
    }

    setTimeout(
      () => {
        current = getRandom();
        selected = undefined;
      },
      selected.symbol === current?.symbol ? 2000 : 4000,
    );
  }

  const questionLabel = $derived(
    current === undefined
      ? "...."
      : mode === "symbol"
        ? current.name
        : current.symbol,
  );
</script>

<div class="p-4">
  <a
    href={resolve("/")}
    class="mb-4 inline-block text-2xl transition hover:opacity-80 active:scale-95"
    aria-label="Go back"
  >
    🔙
  </a>
  <h1 class="mb-6 text-center text-2xl font-semibold sm:text-3xl">
    {mode === "symbol" ? "What is" : "What is the name for"}
    <span class="text-center text-3xl font-bold">
      {questionLabel} ?
    </span>
  </h1>

  <p class="mb-1 text-center text-sm text-gray-500"></p>
  <div
    class="flex h-25 items-center justify-center gap-3 text-3xl font-semibold"
  >
    {#if result === "correct"}
      ✅
      <Confetti x={[-2, 2]} fallDistance="15rem" />
    {:else if result === "wrong"}
      ❌
      <ElementSummary element={selected!} /> is not
    {/if}
    {#if result && current}
      <ElementSummary element={current} />
    {/if}
  </div>
  <PeriodicTable {onClick} {mode} />
  <Score value={score} />
</div>
