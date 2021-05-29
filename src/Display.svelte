<script>
  export let boundArray;
  const updateDisplay = (arr) => {
    let strprep = "";
    for (let i = 0; i < arr.length; i++)
      strprep += `<div style='--order: ${arr[i]}; height: calc(100% / ${
        arr.length + Math.floor(arr.length / 10) + 1
      }); width: calc(var(--order) * 1%); background: rgba(51, 51, 51, 1);' 
	  class='numbers'></div>`;
    return strprep;
  };
  $: children = updateDisplay(boundArray);
</script>

<div class="container">{@html children}</div>

<style>
  .container {
    width: 70vw;
    height: 80vh;
    display: flex;
    margin: 2rem auto;
    justify-content: space-between;
    flex-direction: column;
    background: rgba(30, 30, 30, 1);
    border: 3px solid black;
    border-radius: 2px;
    padding: 2px;
  }
</style>
