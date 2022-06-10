<script context="module">
	import { csvParse } from 'd3-dsv';
	import { csv_data } from './CsvData.svelte';
	
	export const stat_labels = 
				["hp", "atk", "def", "int", "skl", "will", "ref", "fort", 
				 "agility", "dexterity", "strength", "endurance", "squirm",
				 "biotech", "history", "people", "places", "engineering",
				 "computers", "medical", "peopleReading", "deceive", 
				 "manipulate", "sooth", "command", "persuade", "entertain",
				 "perception", "survival", "research", "craft", "zeroG"];
	
	let input_data = csvParse(csv_data);
	export let races = new Map();
	export let classes = new Map();
	
	class SpecializationData {
		constructor(raw_data) {
			this.title = raw_data.title;
			this.type = raw_data.type;
			for (let stat of stat_labels) {
				this[stat] = parseInt(raw_data[stat]);
			}
			
			this.specials = [];
			for (const special of [raw_data.special0, raw_data.special1, raw_data.special2]) {
				if (special != "") {
					this.specials.push(special);
				}
			}
		}
	}
			
	for (const data_row of input_data.values()) {
		let spec_dat =  new SpecializationData(data_row);
		if (spec_dat.type === "race") {
			races.set(spec_dat.title, spec_dat);
		} else if (spec_dat.type === "class") {
			classes.set(spec_dat.title, spec_dat);
		}
	}
			
	export let race_titles = [...races.keys()];
	export let class_titles = [...classes.keys()];
</script>