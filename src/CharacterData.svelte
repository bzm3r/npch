<script context="module">
	import { csvParse } from "d3-dsv";
	import csv_data from "/assets/npch_data.csv?raw";

	export const primaries1 = ["hp", "atk", "def", "init"];
	export const primaries2 = ["skl", "will", "ref", "fort"];
	export const physicals = [
		"Agility",
		"Dexterity",
		"Strength",
		"Zero-G",
		"Stealth",
		"Endurance",
		"Squirm",
	];
	export const socials = [
		"Soothe",
		"Entertain",
		"Deceive",
		"Manipulate",
		"Persuade",
		"Command",
		"People reading",
	];
	export const knowledges = [
		"Biotech",
		"History",
		"People",
		"Places",
		"Engineering",
		"Computers",
		"Medical",
	];
	export const practicals = [
		"Perception",
		"Survival",
		"Research",
		"Craft",
		"Piloting",
	];

	export const all_labels = primaries1
		.concat(primaries2)
		.concat(physicals)
		.concat(socials)
		.concat(knowledges)
		.concat(practicals);

	let input_data = csvParse(csv_data);
	export let races = new Map();
	export let classes = new Map();

	class Special {
		constructor(raw_special_str) {
			let type, str;
			[type, str] = raw_special_str.split(":").map((s) => s.trim());
			this.type = type;
			this.str = str;
		}
	}

	class SpecialsData {
		constructor(raw_specials_str) {
			let specials = raw_specials_str
				.split(";")
				.map((s) => s.trim())
				.filter((s) => s.length > 0)
				.map((s) => new Special(s));

			this.flavor = [];
			this.primary = [];
			this.skill = [];
			this.equipment = [];
			for (const special of specials) {
				if (special.type === "flav") {
					this.flavor.push(special.str);
				} else if (special.type === "pri") {
					this.primary.push(special.str);
				} else if (special.type === "skl") {
					this.skill.push(special.str);
				} else if (special.type === "equip") {
					this.equipment.push(special.str);
				}
			}
		}
	}

	class SpecializationData {
		constructor(raw_data) {
			this.title = raw_data.title;
			this.type = raw_data.type;
			for (let label of all_labels) {
				this[label] = parseInt(raw_data[label]);
			}

			this.specials = new SpecialsData(raw_data.specials);
		}
	}

	for (const data_row of input_data.values()) {
		let spec_dat = new SpecializationData(data_row);
		if (spec_dat.type === "race") {
			races.set(spec_dat.title, spec_dat);
		} else if (spec_dat.type === "class") {
			classes.set(spec_dat.title, spec_dat);
		}
	}

	export let race_titles = [...races.keys()];
	export let class_titles = [...classes.keys()];
</script>
