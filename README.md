# BP.Modules
Modules allow Behavior Programmers to build up a library of knowledge to be easily imported into a different project. A module is build out of different elements. An element needs to be one of the types ```entity```, ```commands```, ```loot_table``` or ```trades```. Elements of the type ```entity``` are independet of the entity type. The user can choose on which entity this part of the module shall be applied.

## Element [type=entity]
The most advanced element of a module. In this element, you describe what you want to change by adding it to the ```replace``` and ```add``` objects or to the "remove" array.

```javascript
{
	"elements": [
		{
			"type": "entity",
			"name": "marker",
			"description": "Mark a location",

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

#### Functionality of "add"
Add components, component_groups and events through the ```add``` object. If a ```component```/```event```/```component_group``` already exists on the entity chosen by the user, a merge conflict gets added to the merge_conflicts.json file.
