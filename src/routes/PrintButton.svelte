<script>
	export let race;
	export let class1;
	export let class2;
	export let class3;

	let disabled = false;
	let print_message = 'Print to PDF';

	$: race, class1, class2, class3, (disabled = false), (print_message = 'Print to PDF');

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
		let concat_underscore = '';

		let pdfs = [];
		pdfs.push(await load_pdf('Blank'));

		if (race != '') {
			pdfs.push(await load_pdf(race));
			if (concat_underscore === '') {
				pdf_name = race;
				concat_underscore = '_';
			} else {
				pdf_name += concat_underscore + class1;
			}
		}

		if (class1 != '') {
			pdfs.push(await load_pdf(class1));
			if (concat_underscore === '') {
				pdf_name = class1;
				concat_underscore = '_';
			} else {
				pdf_name += concat_underscore + class1;
			}
		}

		if (class2 != '') {
			pdfs.push(await load_pdf(class2));
			if (concat_underscore === '') {
				pdf_name = class2;
				concat_underscore = '_';
			} else {
				pdf_name += concat_underscore + class2;
			}
		}

		if (class3 != '') {
			pdfs.push(await load_pdf(class3));
			if (concat_underscore === '') {
				pdf_name = class3;
				concat_underscore = '_';
			} else {
				pdf_name += concat_underscore + class3;
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
		link.download = pdf_name.replaceAll('#', '').replaceAll(' ', '').replaceAll('-', '');
		link.target = '_blank';
		link.href = url;
		link.click();
		URL.revokeObjectURL(url);
	}

	async function handleClick() {
		disabled = true;
		print_message = 'Preparing PDF...';
		try {
			create_character_sheets();
		} finally {
			print_message = 'PDF Sent!';
			await setTimeout(() => {
				disabled = false;
				print_message = 'Print to PDF';
			}, 4000);
		}
	}
</script>

<button on:click={handleClick} {disabled}> {print_message} </button>
