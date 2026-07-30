<script lang="ts">
  import { elements } from "../../elements";
  import ElementCard from "./ElementCard.svelte";
  import type { PeriodicElement } from "../../elements";

  type Props = {
    mode: "symbol" | "name";
    onClick: (element: PeriodicElement) => void;
    onEnter?: (element: PeriodicElement) => void;
    onLeave?: (element: PeriodicElement) => void;
  };
  let { onClick, onEnter, onLeave, mode }: Props = $props();
</script>

<div
  class="mx-auto grid max-w-300 gap-0.5 p-4 md:gap-1.5"
  style="grid-template-columns: repeat(18, minmax(2em, 1fr));"
>
  {#each elements as element}
    <div style="grid-column: {element.col}; grid-row: {element.row};">
      <ElementCard
        {element}
        onClick={() => onClick(element)}
        onEnter={() => onEnter?.(element)}
        onLeave={() => onLeave?.(element)}
        {mode}
      />
    </div>
  {/each}
</div>
