<script>
  import PdfViewer from "./components/PdfViewer.svelte";
  let showPdf = false;

  function onShowPdfClick() {
    showPdf = !showPdf;
  }
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }

  .show {
    display: block;
  }

  .hide {
    display: none;
  }

  .pdf-document-view-container {
    height: 60vh;
    overflow: auto;
    padding: 20px;
    background-color: gray;
  }
</style>

<main>
  <h1>Svelte-js-tools</h1>
  <p>a set of example for common stuff using sveltejs.</p>

  <p>Embed a PDF file in a webPage using pdfjs</p>
  <div>
    <button on:click={onShowPdfClick}>Show PDF</button>
    <div class="pdf-document-view-container {showPdf ? 'show' : 'hide'}">
      <PdfViewer
        pdfDocumentUrl="https://www.ets.org/Media/Tests/GRE/pdf/gre_research_validity_data.pdf" />
    </div>
  </div>
</main>
