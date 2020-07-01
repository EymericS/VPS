# Some tools and triks

## Object & function

### Date

* object : 
	```JS
	const date = new Date( dateISO )
	```
* format :
	```JS
	const dateFormat = { 
		dateStyle: 'medium',
		timeStyle: 'short'
	}
	```
* render :
	```JS
	const readableDate = date.toLocalString(undefined, dateFormat)
	```
* Time interval :
	```JS
	/* Create */
	let timer = window.setInterval(
		() => {
		/	* do somthings */
		},
		1000
	)
	/* Delete */
	windows.clearInterval(timer)
	```
		
### `map()` function

Apply a function to an array

## Template

## Design Patern

* intersection Observer
