<script>
	export let race;
	export let class1;
	export let class2;
	export let class3;

	let disabled = false;

	import { PDFDocument } from 'pdf-lib';

	async function load_pdf(description) {
		const res = await fetch(encodeURIComponent('/' + description + '.pdf'));
		let pdf_buffer = await res.arrayBuffer();
		let pdf = await PDFDocument.load(pdf_buffer);
		return pdf;
	}

	async function create_character_sheets() {
		const result_pdf = await PDFDocument.create();

		let pdf_name = 'blank_char_sheet';
		let progress_hyphen = '';

		let pdfs = [];
		pdfs.push(await load_pdf('Blank'));

		if (race != '') {
			pdfs.push(await load_pdf(race));
			if (progress_hyphen === '') {
				pdf_name = race;
				progress_hyphen = '-';
			} else {
				pdf_name += progress_hyphen + class1;
			}
		}

		if (class1 != '') {
			pdfs.push(await load_pdf(class1));
			if (progress_hyphen === '') {
				pdf_name = class1;
				progress_hyphen = '-';
			} else {
				pdf_name += progress_hyphen + class1;
			}
		}

		if (class2 != '') {
			pdfs.push(await load_pdf(class2));
			if (progress_hyphen === '') {
				pdf_name = class2;
				progress_hyphen = '-';
			} else {
				pdf_name += progress_hyphen + class2;
			}
		}

		if (class3 != '') {
			pdfs.push(await load_pdf(class3));
			if (progress_hyphen === '') {
				pdf_name = class3;
				progress_hyphen = '-';
			} else {
				pdf_name += progress_hyphen + class3;
			}
		}

		for (const pdf of pdfs) {
			let pages = await result_pdf.copyPages(pdf, pdf.getPageIndices());
			for (const page of pages) {
				result_pdf.addPage(page);
			}
		}

		// Serialize the PDFDocument to bytes (a Uint8Array)
		const pdf_bytes = await result_pdf.save();
		save_pdf(pdf_bytes, pdf_name);
	}

	function save_pdf(pdf_bytes, pdf_name) {
		var blob = new Blob([pdf_bytes], { type: 'application/pdf' });
		const url = URL.createObjectURL(blob);
		const link = document.createElement('a');
		link.download = pdf_name.replaceAll('#', '').replaceAll(' ', '');
		link.href = url;
		link.click();
		URL.revokeObjectURL(url);
	}

	async function handleClick() {
		disabled = true;
		try {
			create_character_sheets();
		} finally {
			disabled = false;
		}
	}
</script>

<button on:click={handleClick} {disabled}> Print </button>
