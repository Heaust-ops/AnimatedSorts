<script>
  import Display from "./Display.svelte";
  import bubbleSort from "./algorithms/bubbleSort";
  import mergeSort from "./algorithms/mergeSort";
  import heapSort from "./algorithms/heapSort";
  import quickSort from "./algorithms/quickSort";
  import insertionSort from "./algorithms/insertionSort";
  import Slider from "./Slider.svelte";
  import { run } from "svelte/internal";

  const getRandomArray = (cap) => {
    return Array.from(
      { length: cap },
      () => Math.floor(Math.random() * 100) + 1
    );
  };

  const sleep = (ms) => {
    return new Promise((resolve) => setTimeout(resolve, ms));
  };

  let continueFlag = true;
  let skip = false;
  let running = false;
  const startStop = () => {
    continueFlag = !continueFlag;
  };

  let boundArray;
  let arrayCap = 12;
  $: arrayCap = arrayCap < 5 ? 5 : arrayCap;
  let speed = 2 * arrayCap;
  $: speed = speed < 1 ? 1 : speed;
  $: waitTime = speed > 0 ? (2 / speed) * 1000 : 1000;
  boundArray = getRandomArray(12);
  const resetArray = () => {
    if (!arrayCap) arrayCap = 12;
    if (arrayCap < 5) arrayCap = 12;
    skip = true;
    boundArray = getRandomArray(arrayCap);
  };

  const playSort = async (func) => {
    let i = 0;
    let StateContainer = func(boundArray);
    console.log(StateContainer);
    continueFlag = true;
    if (running) {
      skip = true;
      if (skip) await sleep(2 * waitTime);
    }
    skip = false;
    running = true;
    while (i < StateContainer.length) {
      if (skip) return;
      if (!continueFlag) {
        await sleep(100);
        continue;
      }
      boundArray = StateContainer[i];
      await sleep(waitTime);
      i++;
    }
    running = false;
  };
</script>

<main>
  <div style="display:flex; justify-content: space-around;">
    <div style="display:flex; justify-content: space-around; flex-direction: column;">
      <div style="display: flex; justify-content: space-around;">Number of Bars</div>
      <div>
      <Slider bind:value={arrayCap} />
    </div>

    <div style="display:flex; justify-content: space-around; flex-direction: column;">
      <div style="display: flex; justify-content: space-around;">Speed</div>
      <div>
      <Slider bind:value={speed} />
    </div>
    </div>
    <button on:click={resetArray}> Reset Array</button>
    <button on:click={startStop}> Start / Stop</button>
    <button on:click={() => playSort(bubbleSort)}> Bubble Sort</button>
    <button on:click={() => playSort(mergeSort)}> Merge Sort</button>
    <button on:click={() => playSort(heapSort)}> Heap Sort</button>
    <button on:click={() => playSort(quickSort)}> Quick Sort</button>
    <button on:click={() => playSort(insertionSort)}> Insertion Sort</button>
  </div>

  <Display bind:boundArray />
</main>

<style>

</style>
