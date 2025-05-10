<script>
  import { Canvas, FabricText } from "fabric";
  import { onMount } from "svelte";
  let canvasElement;
  let canvas;
  let imageSrc = null;
  let text;

  // inititalize the canvas here
  onMount(() => {
    canvas = new Canvas(canvasElement);
    canvas.renderAll();
    imageSrc = canvas.toDataURL();
  });

  // Add text to canvas function
  const addText = () => {
    const fabtext = new FabricText(text);
    canvas.add(fabtext);
    canvas.centerObject(fabtext);
    canvas.renderAll();
    imageSrc = canvas.toDataURL();
  };
</script>

<div class="flex min-h-screen">
  <div
    class="flex flex-col items-center justify-center gap-4 p-4 bg-base-200 w-1/3"
  >
    <!-- padding -->
    {#if imageSrc}
      <a href={imageSrc} class="btn btn-accent" download>Download</a>
      <input
        bind:value={text}
        type="text"
        class="input"
        placeholder="Add Text here.."
      />
      <button class="btn btn-accent" onclick={addText}>Add Text</button>
    {:else}
      <p>Loading..</p>
    {/if}
  </div>

  <!-- canvas -->
  <canvas
    class="border-2 border-black"
    bind:this={canvasElement}
    width="500"
    height="500"
  ></canvas>
</div>
