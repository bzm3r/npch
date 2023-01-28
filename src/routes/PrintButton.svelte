<script>
	export let race;
	export let class1;
	export let class2;
	export let class3;

	import { PDFDocument } from 'pdf-lib';

	async function load_pdf(description) {
		const res = await fetch('/' + description + '.pdf');
		let pdf_buffer = await res.arrayBuffer();
		let pdf = await PDFDocument.load(pdf_buffer);
		return pdf;
	}

	async function handleClick() {
		//alert('printing: ' + race + ' ' + class1 + ' ' + class2 + ' ' + class3);

		// Create a new PDFDocument
		const result_pdf = await PDFDocument.create();

		let pdfs = [];
		pdfs.push(await load_pdf('Blank'));

		if (race != '') {
			pdfs.push(await load_pdf(race));
		}

		if (class1 != '') {
			pdfs.push(await load_pdf(class1));
		}

		if (class2 != '') {
			pdfs.push(await load_pdf(class2));
		}

		if (class3 != '') {
			pdfs.push(await load_pdf(class3));
		}

		for (const pdf of pdfs) {
			console.log(pdf);
			await result_pdf.copyPages(pdf, pdf.getPageIndices());
		}

		// Serialize the PDFDocument to bytes (a Uint8Array)
		const pdf_bytes = await result_pdf.save();
		save_pdf(pdf_bytes);
	}

	function save_pdf(pdf_bytes) {
		var blob = new Blob([pdf_bytes], { type: 'application/pdf' });
		const url = URL.createObjectURL(blob);
		const link = document.createElement('a');
		link.download = 'file.md';
		link.href = url;
		link.click();
		URL.revokeObjectURL(url);
	}
</script>

<button on:click={handleClick}> Print </button>
