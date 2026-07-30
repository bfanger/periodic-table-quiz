<script lang="ts">
  import { elements } from "./elements";
  import ElementCard from "./ElementCard.svelte";
  import type { PeriodicElement } from "./elements";

  type Props = {
    onSelect: (element: PeriodicElement | null) => void;
  };
  let { onSelect }: Props = $props();
</script>

<div
  class="mx-auto grid max-w-300 gap-0.5 p-4 md:gap-1.5"
  style="grid-template-columns: repeat(18, minmax(2em, 1fr));"
>
  {#each elements as element}
    <div style="grid-column: {element.col}; grid-row: {element.row};">
      <ElementCard {element} {onSelect} />
    </div>
  {/each}
</div>
