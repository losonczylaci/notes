# DOM

\[TOC\]

## DOM - Document Object Model

[Youtube](https://www.youtube.com/watch?v=0ik6X4DJKCc) - DOM crash course

* DOM intro
* HTML structor
* Examine the Document Object

### MISC

* Within the html file the script can be outsourced to a remote file and could be included

```markup
<script src="dom.js" ></script>
```

* `.innerText` vs `.textContent` the last one disregards the style and  

  there is alos `.innerHtml` as well 

### Query selector

```javascript
document.querySelector()
```

* queryselector will select only the first of the specified element
* can select based on any prWEBoperty \(tagname, id, class...\)
* meant to replace jQuery

### Query selector all

* selecting odd items in a list 

  ```javascript
  var odd = document.querySelectorAll('li:nth-child(odd)')
  ```

### Events

* subscribing to an event
* cancelling default event of submit

