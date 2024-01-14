<script>
  export let mode;
  export let extraClass =  ""; // Add a class prop
</script>

<div class={`card ${extraClass}`}>
  {mode}
</div>