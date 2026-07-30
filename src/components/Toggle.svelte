<script lang="ts">
  type Option = {
    label: string;
    value: string;
  };

  type Props = {
    left: Option;
    right: Option;
    value?: string;
  };
  let { left, right, value = $bindable() }: Props = $props();

  let checked = $derived(value === right.value);

  function toggle() {
    value = checked ? left.value : right.value;
  }

  function selectLeft() {
    value = left.value;
  }

  function selectRight() {
    value = right.value;
  }
</script>

<div class="flex items-center gap-2">
  <button
    class="cursor-pointer border-none bg-transparent text-sm font-medium"
    onclick={selectLeft}
  >
    {left.label}
  </button>
  <button
    class="relative inline-flex w-10 shrink-0 cursor-pointer rounded-full border border-cyan-800 bg-cyan-100 py-px"
    role="switch"
    aria-checked={checked}
    aria-label="Toggle between {left.label} and {right.label}"
    onclick={toggle}
  >
    <span
      class="pointer-events-none inline-block h-5 w-5 translate-x-0.5 rounded-full bg-cyan-800 shadow transition-transform"
      class:translate-x-4={checked}
    ></span>
  </button>
  <button
    class="cursor-pointer border-none bg-transparent text-sm font-medium"
    onclick={selectRight}
  >
    {right.label}
  </button>
</div>
