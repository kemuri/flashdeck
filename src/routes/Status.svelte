<script>
    export let isConnected;
    export let extraClass =  ""; // Add a class prop
  </script>
  <div class={`card ${isConnected ? 'text-green-500' : 'text-red-500'} ${extraClass}`}>
    BT
  </div>