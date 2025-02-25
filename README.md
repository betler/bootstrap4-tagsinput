[![Maintenance](https://img.shields.io/badge/Maintained%3F-my%20own%20needs-yellow.svg)](https://github.com/Nodws/bootstrap4-tagsinput#unmantained-code-as-is) ![License](https://img.shields.io/badge/license-MIT-green)


# Bootstrap Tags Input
Bootstrap Tags Input is a jQuery plugin providing a Twitter Bootstrap user interface for managing tags.


## Usage
Examples can be found [here](http://bootstrap-tagsinput.github.io/bootstrap-tagsinput/examples/).
If page is down, the page was saved to [PDF](https://github.com/betler/bootstrap4-tagsinput/blob/master/Bootstrap%20Tags%20Input.pdf). 

## Features
* Objects as tags
* True multi value
* Typeahead
* Modified for Bootstrap 4 Alpha

## Unmantained code AS-IS
Original note from [@Nodws](https://github.com/Nodws/bootstrap4-tagsinput): 
> Please fork and continue development if you need this plugin, as I only needed to update it for a project and will not continue further support :)

I personally forked this because I'm using it in a personal project and didn't find any updated fork. Just correcting my own needs and detections. I'll try to review any form of contact (issues, pull requests, etc.) but I cannot guarantee

## Examples / Documentation
I will explain here only the modifications I make to the plugin. The rest are explained in "Usage".

### Options

#### inputDataValues
Allows to set data-xx attributes in the generated input.
It needs an array of objects in the format:
```javascript
[{data: 'data-attribute-name', value: 'attribute-value'}]
```
Default: []

Example:
```javascript
$('#inputFieldId').tagsinput({
   inputDataValues: [{data: 'role', value: 'hidden-input'}, {data: 'id', value: 45}]
});
```
Will produce:
```html
<input type="text" data-role="hidden-input" data-id="45" placeholder="">
```

#### enclosingDataValues
Allows to set data-xx attributes in the generated enclosing div.
It needs an array of objects in the format:
```javascript
[{data: 'data-attribute-name', value: 'attribute-value'}]
```
Default: []

Example:
```javascript
$('#inputFieldId').tagsinput({
   enclosingDataValues: [{data: 'content', value: 'taginput'}, {data: 'id', value: 45}]
});
```
Will produce:
```html
<div data-content="tagInput" data-id="45">
```

#### inputClass
Allows to set class attribute for the generated input.
```javascript
inputClass: 'form-control'
```
Default: ''

Example:
```javascript
$('#inputFieldId').tagsinput({
   inputClass: 'form-control'
});
```
Will produce:
```html
<input type="text" class="form-control" placeholder="">
```

#### enclosingClass
Allows to set class attribute for the generated enclosing div.
```javascript
enclosingClass: 'custom-class'
```
Default: 'bootstrap-tagsinput'

Example:
```javascript
$('#inputFieldId').tagsinput({
   enclosingClass: 'bootstrap-tagsinput custom-class'
});
```
Will produce:
```html
<div class="bootstrap-tagsinput custom-class">
```

### Events

#### beforeItemAdd
Event existed in the originally forked project. Original documentation:

> Triggered just before an item gets added. Example:
> ```javascript
> $('input').on('beforeItemAdd', function(event) {
>   // event.item: contains the item
>   // event.cancel: set to true to prevent the item getting added
> });
> ```

The modification made here is to allow the modification of the ```event``` object received in the function as a parameter with two properties to modify or replace the applied css classes to the item:

- ```replaceClass```: text set here will replace the ```class``` attribute in the item added.
- ```addClass```: text set here will be added after the existing ```class``` attribute in the item added.

If both are set, ```replaceClass``` will take precedence.

Example:
```javascript
$('input').on('beforeItemAdd', function(event) {
   if (event.item > 100) {
      event.replaceClass = 'badge badge-error';
      // event.addClass = 'is-invalid';
   }
});
```