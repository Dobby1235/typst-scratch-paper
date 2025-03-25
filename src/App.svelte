<script module lang="ts">
  import * as Typst from '@myriaddreamin/typst.ts/dist/esm/contrib/snippet.mjs'
  import renderer_wasm from '@myriaddreamin/typst-ts-renderer/pkg/typst_ts_renderer_bg.wasm?url'
  import compiler_wasm from '@myriaddreamin/typst-ts-web-compiler/pkg/typst_ts_web_compiler_bg.wasm?url'

  const typst = Typst.$typst

  typst.setCompilerInitOptions({ getModule: () => compiler_wasm })
  typst.setRendererInitOptions({ getModule: () => renderer_wasm })

</script>

<script lang="ts">
  let input = $state('')

  let output: HTMLDivElement


  $effect(() => {
    typst.svg({ mainContent: input }).then(svg => { output.innerHTML = svg })
  })
</script>

<main class="container">
  <div class="panel">
    <textarea id="input" bind:value={input}></textarea>
  </div>
  <div class="panel">
    <div id="output" bind:this={output}></div>
  </div>
</main>

<style lang="scss">
  .container {
    display: flex;
    height: 100vh;

    .panel {
      flex: 1;
      height: 100%;
      padding: 1em;
      box-sizing: border-box;
    }

    #input {
      width: 100%;
      height: 100%;
      resize: none;
      font-family: 'Fira Code', 'Cascadia Code', monospace;
    }
  }
</style>