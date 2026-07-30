<script lang="ts">
  import { colors, type PeriodicElement } from "./elements";

  type Props = {
    element: PeriodicElement;
    onClick: (element: PeriodicElement | null) => void;
    mode: "symbol" | "name";
  };
  let { element, onClick: onSelect, mode = "symbol" }: Props = $props();

  let { bg, text } = $derived(
    colors[element.category] ?? { bg: "bg-gray-100", text: "text-gray-900" },
  );
</script>

<button
  class={`${bg} ${text} aspect-square w-full  p-0.5 text-center transition-all hover:shadow-md ${mode === "name" ? "text-xs" : "text-lg font-semibold"}`}
  onclick={() => onSelect(element)}
>
  {#if mode === "name"}
    <div class="inline-flex flex-wrap justify-center">
      {#if element.name.endsWith("ium")}
        <span>{element.name.slice(0, -3)}</span>
        <span>ium</span>
      {:else}
        {element.name}
      {/if}
    </div>
  {:else}
    {element.symbol}
  {/if}
</button>
