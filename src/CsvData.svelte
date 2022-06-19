<script context="module">
	export let csv_data = String.raw`title,type,hp,atk,def,init,skl,will,ref,fort,Agility,Dexterity,Strength,Piloting,Stealth,Endurance,Squirm,Biotech,History,People,Places,Engineering,Computers,Medical,People reading,Deceive,Manipulate,Soothe,Command,Persuade,Entertain,Perception,Survival,Research,Craft,Zero-G,special0,special1,special2
Archon,race,25,0,0,-2,1,2,-1,2,0,0,0,0,0,0,0,0,5,0,0,0,0,0,0,0,0,0,2,0,0,0,0,0,0,0,Robotic,Immune to fear,IronHeart
Fae,race,19,0,1,2,3,-1,2,1,2,2,0,0,0,0,2,0,0,0,0,0,0,0,0,0,0,0,0,0,3,2,0,0,2,0,+3 in two social checks,
Half-Fae,race,20,0,0,1,3,0,2,0,2,2,0,0,0,0,2,0,0,0,0,0,0,0,0,0,0,0,0,0,2,0,0,0,0,0,+5 vs disease,Dabbler
Homunculi,race,19,0,1,1,3,0,0,0,0,0,0,0,0,0,3,0,0,0,0,0,3,0,0,3,3,0,0,0,3,0,0,0,0,0,Robotic,Intuitive
Human-Streetborn,race,19,1,1,1,2,0,2,0,2,2,0,0,2,0,2,0,0,0,0,0,0,0,0,2,0,0,0,0,0,2,2,0,0,0,+1  reaction,
Human-Aristocrat,race,20,1,0,0,2,2,0,0,0,0,0,0,0,0,0,0,2,4,0,0,0,0,0,0,2,0,2,0,0,0,0,0,0,0,Family Name,Staff
Human-Academic,race,19,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,3,0,0,0,0,0,0,0,0,0,0,0,0,0,3,0,0,Double all bonuses from your first class,
Human-Skyborn,race,20,0,0,0,3,2,2,0,0,0,-3,3,0,0,0,0,0,0,3,0,0,0,0,0,0,0,0,0,0,0,0,0,2,4,Citizenship,
Jotunn,race,23,0,0,0,2,0,0,2,0,0,2,0,0,2,0,0,0,0,0,2,0,0,0,0,0,0,0,0,0,0,2,0,0,0,Hardy,+2 on Combat manuvers
Nix,race,21,0,0,0,2,1,1,1,0,0,0,0,0,0,2,2,2,0,0,0,0,0,2,0,0,2,0,0,0,2,0,0,2,0,Amphibious,+1 Teamwork
Tsuku,race,20,1,0,4,2,0,3,0,0,3,0,3,3,0,0,0,0,0,0,3,0,0,-2,-2,-2,-2,-2,-2,-2,0,0,0,3,3,Robotic,Resistant to heat and radiation
Vesp,race,17,0,0,1,4,3,0,-1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,3,0,0,0,0,0,0,0,0,3,3,0,Bookworm skill rank,+1 charge/+1gland/+3 on class skill
A390# Spider Drone,class,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,Repair robot Minion,
Apothecary,class,1,0,1,0,1,1,1,2,0,0,0,0,0,0,0,2,0,0,0,0,0,2,0,0,0,0,0,0,0,0,0,2,2,0,+2 DC on Biotech,
Bodyguard,class,2,0,2,2,0,1,1,1,0,0,0,0,0,0,0,0,2,2,0,0,0,2,2,0,0,2,0,0,0,2,0,0,0,0,+1 ATK unarmed OR light guns,+1 crit def range
Brute,class,3,2,0,0,0,0,0,2,0,0,4,0,0,2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"+1 ATK if unarmed, or bludgeoning",
Calabrist,class,0,0,0,0,2,1,1,1,0,0,0,2,0,0,0,0,0,0,0,2,0,0,0,0,0,0,0,2,0,0,2,0,2,0,+1 ATK or +1 DEF,+1HP or +1 companion charge,+1 ATK with Signature Weapon
Champion,class,2,0,0,1,0,2,2,2,0,0,0,2,0,2,0,0,0,0,0,0,0,0,0,0,0,0,2,2,0,0,0,0,0,0,+1ATK with big weapons,+ATK or +1 DEF
Changeling,class,1,0,0,1,2,0,0,0,0,0,0,0,0,0,0,1,0,0,0,1,1,1,0,0,0,0,0,0,0,0,1,0,1,0,+2 in one skill of choice,+2 spread over saving throws
Chronographer,class,0,0,0,3,2,2,2,0,0,0,0,0,0,0,0,0,2,0,0,0,0,0,0,0,2,0,0,0,0,0,0,2,0,2,+1 interrupt action,
Con-Artist,class,0,0,1,1,2,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2,2,2,1,1,1,2,0,0,0,0,0,,
Conduit,class,1,0,0,0,3,3,0,0,0,0,0,2,0,0,0,0,0,0,0,0,4,0,0,2,0,0,0,2,0,0,0,2,0,0,,
Crescent Staccato,class,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,flying robot buddy,
Duo,class,0,1,1,0,3,1,1,0,2,0,0,0,0,0,2,0,0,0,0,0,0,0,0,0,0,0,0,0,2,0,0,0,0,0,Paired class,
Fortress,class,5,0,0,0,0,0,0,2,0,0,2,0,0,3,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,+2 ATK with hammers,You provide Cover.
Freerunner,class,0,0,2,1,2,0,2,0,4,0,0,0,2,2,2,0,0,0,0,0,0,0,0,0,0,0,0,0,2,2,0,0,0,4,+1 interupt action,
Goliath Pangolin,class,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,,
Gunslinger,class,1,1,0,2,1,0,2,0,2,2,0,2,0,0,0,0,0,0,0,0,0,0,0,2,0,0,0,0,2,0,0,0,0,0,+1 ATK when dual weilding.,
Hearthoak,class,0,0,0,0,2,0,0,2,0,0,0,0,0,0,0,0,0,0,2,0,0,0,0,0,0,2,0,0,0,0,2,0,2,0,+1 HP or gland at game start,
Impostor,class,0,0,0,0,3,2,0,2,0,0,0,0,0,0,0,0,0,2,0,0,0,0,0,3,0,1,1,0,0,2,0,0,0,0,,
Infiltrator,class,0,0,0,1,3,1,1,1,1,1,0,0,3,0,1,0,0,0,0,0,0,0,0,2,0,0,0,0,0,3,0,1,0,0,,
Jinx,class,0,0,1,1,2,1,1,1,0,0,0,0,0,0,2,2,0,2,0,2,2,0,0,0,2,0,0,0,0,0,0,0,0,0,+ATK on unarmed attacks,
Liaison,class,1,0,0,0,3,2,0,0,0,0,0,0,0,0,0,0,2,2,2,0,0,0,2,0,0,2,0,2,0,2,0,2,0,0,,
Macabre,class,0,2,0,1,1,0,3,0,2,0,0,0,2,0,2,0,0,0,0,0,0,0,0,0,2,0,0,0,0,0,0,0,0,0,+ATK with knives and unarmed,
Maelstrom,class,1,2,0,0,1,2,0,2,0,0,0,0,0,2,0,2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2,+1 ATK elemental damage,
Martial artist,class,2,1,1,0,0,2,1,1,2,2,2,2,2,2,2,0,0,0,0,0,0,0,2,0,0,0,0,0,0,0,0,0,0,0,Your hands are 2d4 weapons,+2 ATK while unarmed
Mender,class,2,0,0,1,1,2,0,2,0,0,0,0,0,0,0,2,0,0,0,2,0,4,0,0,0,2,0,0,0,0,0,0,0,0,,
Paragon,class,1,1,0,0,2,2,0,2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,,
Pilot,class,0,1,0,2,2,0,2,0,0,2,0,4,0,0,0,0,0,0,2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2,+1 ATK and DEF when piloting,
Predator,class,2,1,1,1,0,0,1,1,0,0,2,0,0,2,2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2,0,0,0,,
Ranger,class,0,1,1,0,2,0,1,1,2,0,0,0,2,2,0,0,0,0,2,0,0,0,0,0,0,2,0,0,0,2,2,0,2,0,+ATK knives and rifles,
Shadow,class,0,1,0,1,2,1,2,0,2,3,0,0,3,0,0,0,0,0,0,0,0,0,0,2,2,0,0,0,0,0,0,0,0,0,+1ATK with knives,
Sharpshooter,class,0,2,0,0,2,2,0,0,0,0,0,0,2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,3,2,0,0,0,+1 ATK with rifles,
Ship's Engineer,class,2,0,1,0,2,0,0,0,0,2,2,0,0,0,0,0,0,0,0,4,0,0,0,0,0,0,0,2,0,0,0,0,2,2,,
Strategist,class,2,0,0,3,2,2,0,0,0,0,0,0,0,0,0,0,2,0,0,0,0,0,0,0,0,0,2,2,0,2,0,2,0,0,Strategize,
Swarmmaster,class,1,0,0,2,2,2,0,2,0,0,0,0,0,0,2,2,0,0,0,0,0,0,0,0,2,0,0,0,0,0,0,0,0,0,,
Swordfiend,class,1,1,1,1,1,0,2,0,3,3,1,1,0,0,0,0,0,0,0,0,0,0,0,1,1,0,0,0,1,0,0,0,0,0,+1 ATK when using sword,
Tinker,class,0,1,0,0,3,0,3,0,0,0,0,2,0,0,0,0,0,0,0,3,2,0,0,0,0,0,0,0,0,0,0,2,3,0,+1 charge (Personal or companion),
Wardog,class,3,1,1,0,0,0,0,2,0,0,2,2,0,4,0,0,0,0,0,0,0,0,0,0,0,0,2,0,0,0,2,0,0,0,,
`;
</script>