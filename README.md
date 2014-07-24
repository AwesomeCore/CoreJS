CoreJS
======

Awesome Event Oriented Javascript Framework

#Installing

#API

##Events
Event is a complex event model. 

###Initialization

```javascript
  var Object = {
      FirstExampleEvent : new Core.EventPoint()
    , SecondExampleEvent: new Core.EventPoint()
  }
```

###Firing

```javascript
  var FireObject = {
    fireEvent: function() {
      new Object.FirstExampleEvent({param1: 'param1'});
      new Object.SecondExampleEvent();
    }
  }
```
###Catching

####Single Event Catching
```javascript
var CatchObject = {
  onEvent: function() {
    var event = Core.CatchEvent(Object.FirstExampleEvent);
    
    // event == { param1: 'param1' }
  }
}
```

####Multiple Event Catching
```javascript
var CatchObject = {
  onEvent: function() {
    var event = Core.CatchEvent(Object.FirstExampleEvent, Object.SecondExampleEvent);
    
    if( event instanceof Object.FirstExampleEvent ) {
      // event == { param1: 'param1' }
    } else {
      //
    }
  }
}
```

##Requests

###Initialization

```javascript
  var Object = {
      ExampleRequest: new Core.RequestPoint()
  }
```

###Firing

```javascript
  var FireObject = {
    fireRequest: function() {
      new Object.ExampleRequest({param1: 'param1'}, function(data) {
        console.log(data);
      });
    }
  }
```
###Catching

```javascript
var CatchObject = {
  onRequest: function() {
    var request = Core.CatchRequest(Object.ExampleRequest);
    
    return function(success) {
      //code here
      var data = { answer: 'answer to request', params: request.param1};
      success(data);
    }
  }
}
```

##States

###Description
####Usage
```javascript
 Core.state(state1, state2, ...)
```

####Params
```javascript
  (String) '' // name of the state
```

####Returns
```javascript
 (Object) {
    value: (String)    // current state value
  , go   : (Function)  // method to change state
 }
```

###Examples
####Initialization
```javascript
 var Object = {
   mainState: Core.state('Idle', 'Running', 'Stopped')
 }
```
When the object has been inited, its state goes to the first value of the set.


####Changing State
```javascript
  Object.mainState.go('Running');
```

When state has been changed, the Event `Object.mainState.GoRunning` fires. And it can be catched at any space of the application.

```javascript
 var MiddleObject = {
  getState: function() {
    Core.CatchEvent(Object.mainState.GoRunning, Object.mainState.GoStopped);
    
    if( Object.mainState.value === 'Running' ) {
      // your code here
    }
  }
 }
```
