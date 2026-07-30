<script lang="ts">
  import { Tween } from "svelte/motion";
  let { value }: { value: number } = $props();

  const score = new Tween(0, { duration: 750 });
  let big = $state(false);
  $effect(() => {
    big = true;
    void score.set(value).then(() => {
      big = false;
    });
  });
</script>

<div
  class="absolute top-4 right-6 font-mono font-bold transition-all {big
    ? 'text-3xl text-slate-600'
    : 'text-2xl text-slate-400'}"
>
  {score.current.toFixed(0)}
</div>
