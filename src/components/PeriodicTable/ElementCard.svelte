<script lang="ts">
  import { colors, type PeriodicElement } from "./elements";

  type Props = {
    element: PeriodicElement;
    onSelect: (element: PeriodicElement | null) => void;
  };
  let { element, onSelect }: Props = $props();

  let { bg, text } = $derived(
    colors[element.category] ?? { bg: "bg-gray-100", text: "text-gray-900" },
  );
</script>

<button
  class={`${bg} ${text} aspect-square w-full p-0.5 text-center text-lg font-semibold transition-all hover:shadow-md`}
  onclick={() => onSelect(element)}
>
  {element.symbol}
</button>
