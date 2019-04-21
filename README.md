### This is an  POST Form <h2>
        
_You **can** combine this with your web project_

here you create variables of your form and input, as well as create a new div.

```javascript
	 let form = document.querySelector('.main-form'),
        input = form.getElementsByTagName('input'),
        statusMessage = document.createElement('div');
```
here you can see my form, you can have it differently and classes can be 
with a different name, just remember to change the names of the classes in JavaScripts

```html
	<form action="#" class="main-form">
							
								<label class="popup-form__label" for="phone">
								Enter your phone number:
								</label>
								<input class="popup-form__input" name="phone" type="tel" required placeholder="+48 (750) 321 322">
								<button class="button popup-form__btn">
									Submit your application!
								</button>
						</form>
```

With this line we do not allow our site to reboot.

```javascript
	event.preventDefault();
```
thanks to this line, we indicate that our created div is a child element of our form

```javascript
     targetEvent.appendChild(statusMessage);
```
In this part of the code, the request is configured.

```javascript
	let request = new XMLHttpRequest();
        request.open('POST', 'server.php');
        request.setRequestHeader('Content-type', 'application/json; charset=utf-8');
```
We write data from our targetEvent this is the same as form into a variable formData,
we will re-convert it into the json format and send it to the server
```javascript
	let formData = new FormData(targetEvent);
        
        let obj = {};
        formData.forEach(function (value, key) {
            obj[key] = value;
        });
        
        let json = JSON.stringify(obj);
        
        request.send(json);
```
This function is called after we received changes in the status of our request, 
and whatever the user is experiencing, we give him to understand what is happening 
and whether he could send the form by writing the answers to our created div.
```javascript
request.addEventListener('readystatechange', function () {
            if (request.readyState < 4) {
                statusMessage.innerHTML = message.loading;
            } else if (request.readyState === 4 && request.status == 200) {
                statusMessage.innerHTML = message.success;
            } else {
                statusMessage.innerHTML = message.failure;
            }
        });
```
Well, the most important thing is to call our function by **postServerForm()** by 
sending the form and transmit the data so that the function of **postServerForm()**ц could work

```javascript
form.addEventListener('submit', function (event) {
        let eventForm = event,
            target = event.target;
        postServerForm(eventForm, target);
    });
```


*to use this feature just copy the code from the project and paste it into your project.*
