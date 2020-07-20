<script>
  import pdfjsLib from "pdfjs-dist";
  import pdfjsWorker from "pdfjs-dist/build/pdf.worker.entry";

  export let pdfDocumentUrl = null;
  let pdfPagesContainer;

  let pdfRenderedPagesCount = 0;
  let pdfNumPages = 0;
  let pdf;

  var loadingTask = pdfjsLib.getDocument(pdfDocumentUrl);
  loadingTask.promise.then(function(pdfDocument) {
    pdf = pdfDocument;
    pdfNumPages = pdfDocument.numPages;
    renderPages();
  });

  function renderPages() {
    for (let index = 0; index < pdfNumPages; index++) {
      pdf.getPage(index + 1).then(function(pdfPage) {
        var viewport = pdfPage.getViewport({ scale: 2.0 });
        let canvas = document.createElement("canvas");
        canvas.width = viewport.width;
        canvas.height = viewport.height;
        canvas.setAttribute("style", "border:none; width: 100%");
        var ctx = canvas.getContext("2d");
        pdfPage.render({
          canvasContext: ctx,
          viewport: viewport
        });
        pdfPagesContainer.append(canvas);
      });
    }
  }
</script>

<style>
  .pdf-document-view {
    width: 100%;
    border: none;
    direction: ltr;
    margin-bottom: 20px;
  }
</style>

<div bind:this={pdfPagesContainer} class="pdf-document-view" />
