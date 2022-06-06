<script context="module">
	import { csvParse } from 'd3-dsv';
	import { csv_data } from './CsvData.svelte';
	
	const stat_labels = 
				["hp", "atk", "def", "int", "skl", "will", "ref", "fort", 
				 "agility", "dexterity", "strength", "endurance", "squirm",
				 "biotech", "history", "people", "places", "engineering",
				 "computers", "medical", "peopleReading", "deceive", 
				 "manipulate", "sooth", "command", "persuade", "entertain",
				 "perception", "survival", "research", "craft", "zeroG"];
	
	class SpecializationData {
		constructor(raw_specialization_data) {
			this.title = raw_specialization_data.title;
			this.type = raw_specialization_data.type;
			stat_labels.forEach(stat => this[stat] = parseInt(raw_specialization_data.stat));
			this.specials = [raw_specialization_data.special0, raw_specialization_data.special1];
		}
	}
	
	class Specializations {
		constructor(csv_data) {
			let input_data = csvParse(csv_data);
			this.races = new Map();
			this.classes = new Map();
			
			for (const [index, entry] of input_data.entries()) {
				if (entry["type"] == "race") {
					this.races.set(entry["title"], new SpecializationData(entry));
				} else if (entry["type"] == "class") {
					this.classes.set(entry["title"], new SpecializationData(entry));
				}
			}
			
			this.race_titles = [...this.races.keys()];
			this.class_titles = [...this.classes.keys()];
		}
		
		getRace(race) {
			return this.races.get(race);
		}
	}
	
	export let specializations = new Specializations(csv_data);
	export let race_titles = specializations.race_titles;
	export let class_titles = specializations.class_titles;
</script>
