# jQuery confirm modal

This plugin replaces the default javascript confirm box by using bootstrap's 4 modal component. Demo available [here.](https://tcja.github.io/jQuery-confirm-modal/)

## Dependencies

#### *bootstrap 4.xx (both css and js)*
#### *jquery 3.xx*

## How to install
Add the following code for the dependencies in your `HEAD` tag :

```html
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
<script src="https://code.jquery.com/jquery-3.4.1.min.js" integrity="sha256-CSXorXvZcTkaix6Yvo6HppcZGetbYMGWSFlBw8HfCJo=" crossorigin="anonymous"></script>
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js" integrity="sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM" crossorigin="anonymous"></script>
```
then add the plugin :
```html
<script src="jquery.confirmModal.min.js"></script>
```

## Fire the plugin

We need to make sure that the DOM is ready before we implement the plugin, in this example we use the click event method that jQuery provides.
```html
<script type="text/javascript">
  $(function(){         
    $('.confirmModal').click(function(e) {
      e.preventDefault();              
      $.confirmModal('Are you sure you want to do this?', function(el) {
        alert('OK was clicked!');
        //do something...
      });
    });          
  });
</script>
```
The **first argument** is the *message* we want to display, the **second argument (optional)** provides *custom options for a specific modal* and **the third one** is the *callback function* with the current clicked element passed as an argument (in this case the element being `<a href="" class="confirmModal">click</a>`).

By default, the plugin is set with the following options : 
* The default locale is english
* There is no header text above the message displayed => `messageHeader: '&nbsp;'`
* The modal's width is automatically sized according to the message displayed => `modalBoxWidth: 'auto'`
* The modal displays instantly without any fade animation => `fadeAnimation: false`
* The modal displays on the top of the page => `modalVerticalCenter: false`
* The background is dark when the modal is displayed (bootstrap 4 default modal background) => `backgroundBlur: false`
* There is no auto-focus on the "OK" button => `autoFocusOnConfirmBtn: false`

but you can change all those options by two ways, the first one by setting a global default behavior and the second one by specifying a custom behavior for a specific modal (if set alongside global defaults, they will overwrite them), the global variable for the default options is the following : `$defaultsConfirmModal`, here is an example of the list of all the options you can change :
```javascript
//$defaultsConfirmModal sets a global default behavior for all confirm modals
$defaultsConfirmModal = {
  confirmButton: 'Confirm', //changes the confirm button locale
  cancelButton: 'Cancel', //changes the cancel button locale
  messageHeader: 'Call to action', //any text you want to display above the main message
  modalBoxWidth: '365px', //set a fixed width in px/rem/em
  modalVerticalCenter: true, //the modal will be vertically aligned
  fadeAnimation: true, //the modal will have a fade in and fade out animation
  backgroundBlur: true, //if set to true : the plugin assumes that the content of your website
                        //is wrapped in a div with the class name "container" and applies a blur of 0.1rem,
                        //if you don't use such a wrapper or the wrapper has another name, you can pass an array
                        //with your own selectors that you wish to blur and also set your own blur weight in px/rem (optional)
                        //like that : ['#header, #content, #footer', '3px']
  autoFocusOnConfirmBtn: true //when the modal is displayed, there will be an auto-focus on the "OK"button
                              //so the user can press enter instead of clicking on the button
};
```

An example speaks better for itself :
```html
<script type="text/javascript">
  $(function() {
    //Let's say we want by default all modals to have french locale, to not display
    //any header text, we want a fixed width of 500px, we want the fade animation
    //and we want the auto-focus on the "confirm" button
    $defaultsConfirmModal = {
      confirmButton: 'Confirmer',
      cancelButton: 'Annuler',
      modalBoxWidth: '500px',
      fadeAnimation: true,
      autoFocusOnConfirmBtn: true
    };

    $('.anotherConfirmModal').click(function(e) {
      e.preventDefault();
      //Now, we want to change the default behavior we set earlier but just for this specific modal, 
      //we'll set a text header, we don't want the auto-focus on the button, we'll center the modal vertically and we want to blur
      //the background, as stated previously those new values will overwrite the default ones set with $defaultsConfirmModal variable
      var options = {
        messageHeader: 'Call to action',
        modalVerticalCenter: true,
        backgroundBlur: ['#header_wrap, #main_content_wrap, #footer_wrap'],
        autoFocusOnConfirmBtn: false
      };
      $.confirmModal('Are you sure you want to do this?', options, function(el) {
        alert('Yay!! You confirmed!');
        //do something...
      });
    });
  
    $('.yetAnotherConfirmModal').click(function(e) {
      e.preventDefault();
      //Here we don't specify any custom options so the default values from $defaultsConfirmModal will apply,
      //if there is no $defaultsConfirmModal variable then the plugin's default values will apply
      $.confirmModal('Are you really sure you want to do this?', function(el) {
        alert('Gratz, You confirmed!');
        //do something...
      });
    });
  });
</script>
```

## License

Released under the **MIT License**
