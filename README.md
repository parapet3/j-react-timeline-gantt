# react-gantt-timeline

[![MIT License](https://img.shields.io/npm/l/react-list.svg?style=flat-square)](http://opensource.org/licenses/MIT)

A react timeline gantt component fork.

## About

Go look at the original https://github.com/guiqui/react-timeline-gantt

## Installation

```bash
npm install react-gantt-timeline
```

The component has the following dependencies: moment, react-sizeme

## Getting started

The first thing to once the component has been install and all it dependencies is create the data that the timeline component consume.The time line has two data providers **data** and **links**.

**Data** :is an array of objects that contains the task to be shown. Each one of the object that are part of the array need to have the following compulsory fields

| Property         |     value     | Descriptions                         |
| ---------------- | :-----------: | :----------------------------------- |
| id               | String/Number | An unique identifier for the class   |
| start            |     Date      | The start date of the task           |
| end              |     Date      | The end date of the task             |
| name             |    String     | The name of the task to be diplayed  |
| color (optional) |    String     | The color of the task to be diplayed |

An example of data definition:

```javascript
let data = [
  { id: 1, start: new Date(), end: new Date() + 1, name: "Demo Task 1" },
  { id: 2, start: new Date(), end: new Date() + 1, name: "Demo Task 2" }
];
```

**Links** :is also an array of objects that contains links between task. Each one of the object that are part of the array need to have the following compulsory fields:

| Property |     value     | Descriptions                       |
| -------- | :-----------: | :--------------------------------- |
| id       | String/Number | An unique identifier for the class |
| start    | String/Number | The id of the start task           |
| end      | String/Number | The id of the end task             |

An example of data definition:

```javascript
let links = [
  { id: 1, start: 1, end: 2 },
  { id: 2, start: 1, end: 3 }
];
```

Once the data is define we just need to declare the component and populate it with both data providers.

```javascript
<TimeLine data={data} links={links} />
```

## Handling Inserts,Updates and Deletes

The React-timeline-gantt was build to be use under a Flux architecture, this means that the component should not be managing the state of the application, is up the store and only the store to modify the state of the application. What our component does is to give you callbacks to know when the component is asking for a change.

The TimeLine component is responsible for two things:

- Updating task:Changing name ,start and end date
- Creating Links

Adding,Deleting Task or links can be manage with logic outside the component.
For this reason the react-timeline-gantt component provides the following callbacks:

| name         |          params          |                                                                                                                                           Descriptions |
| ------------ | :----------------------: | -----------------------------------------------------------------------------------------------------------------------------------------------------: |
| onCreateLink |       link:Object        |                                                      This callback is trigger when the component is notifying the creating of a link between two tasks |
| onUpdateTask | task:Object,props:Object | This callback is trigger when the component is notifying the updating of a Task, Sen the task we want to changes, and the properties we want to change |
| onSelectItem |       item:Object        |                                                                         This callback is trigger when an item is selected this can be a task or a link |

## Paging

Paging is manage using the event onHorizonChange.The timeline component preload a certain date range of data, once the user start scrolling when the timeline realise that needs data for a new range, it trigger the onHorizonChange event.
This method then can be use to support serverside paging or client filtering.

| name            |     params     |                                                                                               Descriptions |
| --------------- | :------------: | ---------------------------------------------------------------------------------------------------------: |
| onHorizonChange | start,end:Date | This callback is trigger when the component is notifying that needs to load data for a new range of dates. |

## Customisation

To customise the look and feel the react-timeline-gantt component provides a configuration object that can be pass as a property.
Here is the structure of the config object :

```javascript
{
	header:{ //Targert the time header containing the information month/day of the week, day and time.
		top:{//Tartget the month elements
			style:{backgroundColor:"#333333"} //The style applied to the month elements
		},
		middle:{//Tartget elements displaying the day of week info
			style:{backgroundColor:"chocolate"}, //The style applied to the day of week elements
			selectedStyle:{backgroundColor:"#b13525"}//The style applied to the day of week elements when is selected
		},
		bottom:{//Tartget elements displaying the day number or time
			style:{background:"grey",fontSize:9},//the style tp be applied
			selectedStyle:{backgroundColor:"#b13525",fontWeight:  'bold'}//the style tp be applied  when selected
		}
	},
	taskList:{//the right side task list
		title:{//The title od the task list
			label:"Projects",//The caption to display as title
			style:{backgroundColor:  '#333333',borderBottom:  'solid 1px silver',
				   color:  'white',textAlign:  'center'}//The style to be applied to the title
		},
		task:{// The items inside the list diplaying the task
			style:{backgroundColor:  '#fbf9f9'}// the style to be applied
		},
		verticalSeparator:{//the vertical seperator use to resize he width of the task list
			style:{backgroundColor:  '#333333',},//the style
			grip:{//the four square grip inside the vertical separator
				style:{backgroundColor:  '#cfcfcd'}//the style to be applied
			}
		}
	},
	dataViewPort:{//The are where we display the task
		rows:{//the row constainting a task
			style:{backgroundColor:"#fbf9f9",borderBottom:'solid 0.5px #cfcfcd'}
			},
		task:{the task itself
			showLabel:false,//If the task display the a lable
			style:{position:  'absolute',borderRadius:14,color:  'white',
				   textAlign:'center',backgroundColor:'grey'},
			 selectedStyle:{}//the style tp be applied  when selected
		}
	},
	links:{//The link between two task
		color:'black',
		selectedColor:'#ff00fa'
	}
}
```

Once the object is defined we just need to pass the config object to the timeline config property.

```javascript
<TimeLine data={data} links={links} />
```

## Other properties

| Property | value  |                                                           Descriptions |
| -------- | :----: | ---------------------------------------------------------------------: |
| mode     | string | set the zoom level.The possible values are:"month","week","day","year" |  |
