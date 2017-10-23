Grid component
==============

[![build status](https://img.shields.io/travis/spasdk/component-grid.svg?style=flat-square)](https://travis-ci.org/spasdk/component-grid)
[![npm version](https://img.shields.io/npm/v/spa-component-grid.svg?style=flat-square)](https://www.npmjs.com/package/spa-component-grid)
[![dependencies status](https://img.shields.io/david/spasdk/component-grid.svg?style=flat-square)](https://david-dm.org/spasdk/component-grid)
[![devDependencies status](https://img.shields.io/david/dev/spasdk/component-grid.svg?style=flat-square)](https://david-dm.org/spasdk/component-grid?type=dev)
[![Gitter](https://img.shields.io/badge/gitter-join%20chat-blue.svg?style=flat-square)](https://gitter.im/DarkPark/spasdk)


Grid is a component to build user interface, an instance of [Component](https://github.com/spasdk/component) module.


## Installation ##

```bash
npm install spa-component-grid
```


## Usage ##

Add the singleton to the scope:

```js
var Grid = require('spa-component-grid');
```

Create instance with custom config:

```js
var grid = new Grid({
    data: [
        [1,   2,  3, {value: '4;8;12;16', focus: true, rowSpan: 4}],
        [5,   6,  7],
        [9,  10, 11],
        [13, 14, {value: 15, disable: true}]
    ],
    render: function ( $item, data ) {
        $item.innerHTML = '<div>' + (data.value) + '</div>';
    },
    cycleX: false
});
```

For navigation map implementation and tests see {@link https://gist.github.com/DarkPark/8c0c2926bfa234043ed1}.

Each data cell can be either a primitive value or an object with these fields:

Name    | Description
---- | -----
value   | actual cell value to render
colSpan | amount of cells to merge horizontally
rowSpan | amount of cells to merge vertically
mark    | is it necessary or not to render this cell as marked
focus   | is it necessary or not to render this cell as focused
disable | is it necessary or not to set this cell as disabled


### Constructor config ###

Name | Type | Default value | Description
----- | ----- | ------------- | -------------
data=[] | Array[] | [] | component data to visualize
render | Function | default render | method to build each grid cell content
cycleX | Boolean | true | allow or not to jump to the opposite side of line when there is nowhere to go next
cycleY | Boolean | true | allow or not to jump to the opposite side of column when there is nowhere to go next
provider | Object | null | data provider
sizeX | Number | null | grid columns count
sizeY | Number | null | grid rows count

### Methods ###

#### .normalize( data ) ####

Make all the data items identical. 
Wrap to objects if necessary and add missing properties.

Param name | Type | Description
----- | ----- | ------------- 
data | Array[] | Data user 2-dimensional array
{return} | Array[] | Reworked incoming data


#### .fill( map, posX, posY, dX, dY [, ...] ) ####

Fill the given rectangle area with value.

Param name | Type | Description
----- | ----- | ------------- 
map | Array[] | link to navigation map
posX | Number | current horizontal position
posY | Number | current vertical position
dX | Number | amount of horizontal cell to fill
dY | Number | amount of vertical cell to fill
* | * | value filling data

#### .map( data ) ####

Create a navigation map from incoming data.

Param name | Type | Description
----- | ----- | ------------- 
data | Array[] | data user 2-dimensional array of objects
{return} | Array[] | current horizontal position

#### .move( direction ) ####

Move focus to the given direction.

Param name | Type | Description
----- | ----- | ------------- 
direction | Number | direction arrow key code

#### .focusItem( $item ) ####

Highlight the given DOM element as focused.
Remove focus from the previously focused item.

Param name | Type | Description
----- | ----- | ------------- 
$item | Node or Element | element to focus
$item.x | Number | the item horizontal position
$item.y | Number | the item vertical position
{return} | Boolean| operation status

#### .markItem( $item, state ) ####

Set item state and appearance as marked.

Param name | Type | Description
----- | ----- | ------------- 
$item | Node or Element | element to focus
state | Boolean | true - marked, false - not marked


## Development mode ##

> There is a global var `DEVELOP` which activates additional consistency checks and protection logic not available in release mode.


## Contribution ##

If you have any problem or suggestion please open an issue [here](https://github.com/spasdk/component-grid/issues).
Pull requests are welcomed with respect to the [JavaScript Code Style](https://github.com/DarkPark/jscs).


## License ##

`spa-component-grid` is released under the [MIT License](license.md).
