# BP.Modules
Modules allow Behavior Programmers to build up a library of knowledge to be easily imported into a different project. A module is build out of different elements. An element needs to be one of the types ```entity```, ```commands```, ```loot_table``` or ```trades```. Elements of the type ```entity``` are independet of the entity type. The user can choose on which entity this part of the module shall be applied.

## How do I load modules?
Modules are fully integrated into the next version of MCPacker. You can access the module menu by pressing "ctrl+L" or by using the menubar.

## Creating modules
In order to create a module, add a JSON file describing your module into the modules folder of this repository. You then need to add your module to the module_definitions.json file in this repository. Make sure to choose a descriptive name and add a good description.

### Element [type=entity]
The most advanced element of a module. In this element, you describe what you want to change by adding it to the ```replace``` and ```add``` objects or to the "remove" array.
Order of execution: ```replace``` --> ```add``` --> ```remove```

```javascript
{
	"elements": [
		{
			"type": "entity",
			"name": "[descriptive name]",
			"description": "[description here]",

			"replace": {
				"components": {
				},
				"component_groups": {
				},
				"events": {
				}
			},
			"add": {
				"components": {
				},
				"component_groups": {
				},
				"events": {
				}
			},
			"remove": {
				"components": [ ],
				"component_groups": [ ],
				"events": [ ]
			}
			
		}
	]
}
```

###### Functionality of ```add```
Add components, component_groups and events through the ```add``` object. If a ```component```/```event```/```component_group``` already exists on the entity chosen by the user, a merge conflict gets added to the merge_conflicts.json file (path: your_chosen_bp_path/merge_conflicts.json). You won't loose your ```component```/```event```/```component_group``` in this case.

###### Functionality of ```replace```
```replace``` currently replaces the whole ```components```/```events```/```component_groups``` object of the chosen entity with the one defined. If you want to start your module with a blank entity, this is the way to go...

###### Functionality of ```remove```
Define within ```remove``` object which ```components```/```events```/```component_groups``` of the chosen entity shall be removed. Only the name is required! ```remove``` can currently NOT remove components in component_groups.

### Element [type=loot_table]
Define a whole loot table to be imported upon loading the module in this element. The ```name``` attribute changes the name of the file. 
Path of the loot table: loot_tables/{name}.json

### Element [type=trades]
Define a whole trading table to be imported upon loading the module in this element. The ```name``` attribute changes the name of the file. 
Path of the trading table: trading/{name}.json

### Element [type=commands]
Define a command system by using the type ```commands```. The commands get outputted into a commands.txt file after loading the module. This file should open by default (path: your_chosen_bp_path/commands.txt)
