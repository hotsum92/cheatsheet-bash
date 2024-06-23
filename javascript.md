
## monitor event

##### all event

```javascript

//listen to all events
monitorEvents(window);

//stop listening
unmonitorEvents(window);

```

##### specific event

```javascript

//start listening
monitorEvents(window,"submit");

//stop listening
unmonitorEvents(window,"submit");

```

##### select element

```javascript

monitorEvents($0, "click");

monitorEvents(document.body.querySelectorAll('input'));

```

## remove event

##### remove all event

```javascript

getEventListeners().click.forEach((e)=>{e.remove()})

```

##### remove all timer

```

var maxId = setTimeout(function(){}, 0);
for(var i=0; i < maxId; i+=1) { 
    clearTimeout(i);
}


```

## print

##### print all properties

```javascript

console.log({ "element": $0 });

```
