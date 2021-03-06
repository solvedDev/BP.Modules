# BP.Modules
Modules allow Behavior Programmers to build up a library of knowledge to be easily imported into a different project. A module is build out of different elements. An element needs to be one of the types ```entity```, ```commands```, ```loot_table``` or ```trades```. Elements of the type ```entity``` are independet of the entity type. The user can choose on which entity this part of the module shall be applied.

## How do I load modules?
Modules are fully integrated into the next version of MCPacker. You can access the module menu by pressing "CTRL+L" or by using the menubar.

## Creating modules
In order to create a module, add a JSON file describing your module into the modules folder of this repository. You then need to also add your module to the module_definitions.json file. Make sure to choose a descriptive name and add a good description.

### Element [type=entity]
The most advanced element in a module. In this element, you describe what you want to change by adding it to the ```replace``` and ```add``` objects or to the ```remove``` array. Every change made by the module system is reversible as a changelog file is generated. You can find the changelog for each module in your chosen behavior pack folder saved as a file with the name "changelog_{module name}.json".
Order of execution: ```replace``` --> ```remove``` --> ```add```

```javascript
{
	"elements": [
		{
			"type": "entity",
			"name": "[descriptive name]",
			"description": "[description here]",

			"replace": {
				"replace_group_by_group": false,
				
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
				"parse_groups": false,
				
				"components": [ ],
				"component_groups": [ ],
				"events": [ ]
			}
			
		}
	]
}
```

###### Functionality of ```add```
Add components, component_groups and events through the ```add``` object. If a ```component```/```event```/```component_group``` already exists on the entity chosen by the user, a change objects gets added to the changelog_{module name}.json file (path: your_chosen_bp_path/changelog_{module name}.json). You won't loose your ```component```/```event```/```component_group``` in this case.

###### Functionality of ```replace```
```replace``` currently replaces the whole ```components```/```events```/```component_groups``` object of the chosen entity with the one defined. If you want to start your module with a blank entity, this is the way to go... You can use the ```replace_group_by_group``` argument (accepts ```true```/```false```; default: ```false```) to toggle whether you want to replace the whole ```component_groups``` object (= ```false```) or you want to parse the ```component_groups``` defined and replace only the ones which already exists on the entity. If a defined ```component_group``` is not part of the chosen entity, it won't be added. In order to add a ```component_group```, use the ```add```-section of an element.

###### Functionality of ```remove```
Define within ```remove``` object which ```components```/```events```/```component_groups``` of the chosen entity shall be removed. Only the name is required! The ```parse_groups``` argument toggles whether components shall also be removed out of component groups. Accepted values are ```true```/```false```; the default value is ```false```.


### Element [type=loot_table]
Define a whole loot table to be imported upon loading the module in this element. The ```name``` attribute changes the name of the file. 
Path of the loot table: loot_tables/{name}.json

```javascript
{
	"elements": [
		{
			"type": "loot_table",
			"name": "example loot",
			"loot_table": {
				"pools": [
					"..."
				]
			}
		}
	]
}
```


### Element [type=trades]
Define a whole trading table to be imported upon loading the module in this element. The ```name``` attribute changes the name of the file. 
Path of the trading table: trading/{name}.json

```javascript
{
	"elements": [
		{
			"type": "trades",
			"name": "example trade",
			"trades": {
				"tiers": [
					"..."
				]
			}
		}
	]
}
```


### Element [type=commands]
Define a command system by using the type ```commands```. The commands end up in a commands.txt file after loading the module. This file should open by default (path: your_chosen_bp_path/commands.txt).

```javascript
{
	"elements": [
		{
			"type": "commands",
			"commands": [
				{
					"command": "/testfor @e[type=example]",
					"type": "repeating",
					"is_conditional": false,
					"description": "test_description"
				},
				{
					"command": "/say Found example...",
					"type": "chain",
					"is_conditional": true,
					"description": "test_description"
				}
			]
		},
		{
			"type": "commands",
			"commands": [
				{
					"command": "/say Loaded",
					"type": "impulse",
					"is_conditional": false,
					"description": "test_description"
				}
			]
		}
	]
}
```
