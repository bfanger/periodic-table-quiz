<script lang="ts">
  import { colors, type PeriodicElement } from "../../elements";

  type Props = {
    element: PeriodicElement;
    mode: "symbol" | "name";
    onClick?: () => void;
    onEnter?: () => void;
    onLeave?: () => void;
  };
  let { element, mode = "symbol", onClick, onEnter, onLeave }: Props = $props();

  let style = $derived(
    colors[element.category] ?? { bg: "bg-gray-100", text: "text-gray-900" },
  );
  let highlight = $state(false);

  function split(
    elementName: string,
  ): { prefix: string; suffix: string } | undefined {
    for (const ending of ["ium", "ine", "num", "rus", "son"]) {
      if (elementName.endsWith(ending)) {
        return { prefix: elementName.slice(0, -ending.length), suffix: ending };
      }
    }
    return;
  }

  let timer: number;
  function onkeydown(e: KeyboardEvent) {
    clearTimeout(timer);
    highlight = false;
    if (element[mode][0]!.toLowerCase() === e.key.toLowerCase()) {
      highlight = true;
      timer = window.setTimeout(() => {
        highlight = false;
      }, 1500);
    }
  }
</script>

<button
  class={`${highlight ? "bg-gray-700 text-white" : `${style.bg} ${style.text} duration-1000`} aspect-5/4 w-full rounded-sm p-0.5 text-center transition-colors hover:shadow-md ${mode === "name" ? "text-xs" : "text-lg font-semibold"}`}
  onclick={onClick}
  onmouseenter={onEnter}
  onmouseleave={onLeave}
>
  {#if mode === "name"}
    {@const splitName = split(element.name)}

    <div class="inline-flex flex-wrap justify-center leading-none">
      {#if splitName}
        <span>{splitName.prefix}</span>
        <span>{splitName.suffix}</span>
      {:else}
        {element.name}
      {/if}
    </div>
  {:else}
    {element.symbol}
  {/if}
</button>
<svelte:window {onkeydown} />
