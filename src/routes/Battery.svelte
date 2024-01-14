<script>
    export let batteryLevel;
    export let extraClass =  ""; // Add a class prop
  </script>
  
  <div class={`card ${extraClass}`}>
    Battery: {batteryLevel}%
  </div>