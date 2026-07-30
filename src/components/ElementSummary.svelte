<script lang="ts">
  import type { PeriodicElement } from "../elements";
  import ElementCard from "./PeriodicTable/ElementCard.svelte";

  let { element }: { element: PeriodicElement } = $props();
</script>

<div class="mt-4 flex justify-center">
  <div class="rounded-lg border border-gray-300 bg-white p-4 shadow-sm">
    <div class="flex items-center gap-3">
      <div class="w-16">
        <ElementCard mode="symbol" {element} />
      </div>
      <div>
        <h3 class="text-xl font-semibold">{element.name}</h3>
        <!-- <p class="text-sm opacity-50">{element.category}</p> -->
      </div>
    </div>
  </div>
</div>
