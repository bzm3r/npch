<script context="module">
	import { csvParse } from 'd3-dsv';
	import csv_data from '$lib/npch_data.csv?raw';

	export const primaries1 = ['hp', 'atk', 'def', 'init'];
	export const primaries2 = ['skl', 'will', 'ref', 'fort'];
	export const primaries3 = ['Charges', 'Glands'];
	export const physicals = [
		'Agility',
		'Dexterity',
		'Strength',
		'Zero-G',
		'Stealth',
		'Endurance',
		'Squirm'
	];
	export const socials = [
		'Soothe',
		'Entertain',
		'Deceive',
		'Manipulate',
		'Persuade',
		'Command',
		'People reading'
	];
	export const knowledges = [
		'Biotech',
		'History',
		'People',
		'Places',
		'Engineering',
		'Computers',
		'Medical'
	];
	export const practicals = ['Perception', 'Survival', 'Research', 'Craft', 'Piloting'];

	export const all_labels = primaries1
		.concat(primaries2)
		.concat(primaries3)
		.concat(physicals)
		.concat(socials)
		.concat(knowledges)
		.concat(practicals);

	let input_data = csvParse(csv_data);
	export let races = new Map();
	export let classes = new Map();

	function parse_special_str(special_str) {
		let splits = special_str
			.split(';')
			.map((s) => s.trim())
			.filter((s) => s.length > 0);
		return [...splits];
	}

	class SpecialsData {
		constructor(primary_str, skills_str, flavor_str, equipment_str) {
			this.primary = parse_special_str(primary_str);
			this.skill = parse_special_str(skills_str);
			this.flavor = parse_special_str(flavor_str);
			this.equipment = parse_special_str(equipment_str);
		}
	}

	class SpecializationData {
		constructor(raw_data) {
			this.title = raw_data.title;
			this.type = raw_data.type;
			for (let label of all_labels) {
				this[label] = parseInt(raw_data[label]);
			}

			this.specials = new SpecialsData(
				raw_data.specials_primary,
				raw_data.specials_skill,
				raw_data.specials_flavor,
				raw_data.equipment
			);
		}
	}

	for (const data_row of input_data.values()) {
		let spec_dat = new SpecializationData(data_row);
		if (spec_dat.type === 'race') {
			races.set(spec_dat.title, spec_dat);
		} else if (spec_dat.type === 'class') {
			classes.set(spec_dat.title, spec_dat);
		}
	}

	export let race_titles = [...races.keys()];
	export let class_titles = [...classes.keys()];
</script>
