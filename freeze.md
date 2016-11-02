# Object.freeze() #

## Definition ##
The *Object.freeze()* method freezes an object: that is, prevents new properties from being added to it; prevents existing properties from being removed; and prevents existing properties, or their enumerability, configurability, or writability, from being changed. In essence the object is made effectively immutable. The method returns the object being frozen.

## Need for this Standard ##
To prevent new properties being added and already existing properties from being removed.<br/>

    Object.freeze(obj)

Nothing can be added to or removed from the properties set of a frozen object. Any attempt to do so will fail, either silently or by throwing a TypeError exception (most commonly, but not exclusively, when in strict mode).

## Usefulness of this standard ##
Values cannot be changed for data properties. Accessor properties (getters and setters) work the same (and still give the illusion that you are changing the value). Note that values that are objects can still be modified, unless they are also frozen.

    var obj = {
      prop: function() {},
      foo: 'bar'
    };
    
    // New properties may be added, existing properties may be changed or removed
    obj.foo = 'baz';
    obj.lumpy = 'woof';
    delete obj.prop;
    
    // Both the object being passed as well as the returned object will be frozen.
    // It is unnecessary to save the returned object in order to freeze the original.
    var o = Object.freeze(obj);
    
    o === obj; // true
    Object.isFrozen(obj); // === true
    
    // Now any changes will fail
    obj.foo = 'quux'; // silently does nothing
    obj.quaxxor = 'the friendly duck'; // silently doesn't add the property
    
    // ...and in strict mode such attempts will throw TypeErrors
    function fail(){
      'use strict';
      obj.foo = 'sparky'; // throws a TypeError
      delete obj.quaxxor; // throws a TypeError
      obj.sparky = 'arf'; // throws a TypeError
    }
    
    fail();
    
    // Attempted changes through Object.defineProperty will also throw
    Object.defineProperty(obj, 'ohai', { value: 17 }); // throws a TypeError
    Object.defineProperty(obj, 'foo', { value: 'eit' }); // throws a TypeError
        



## References ##
[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)


## Point of Contact ##
Bharath Kalagotla<br/>
[bkalagotla@deloitte.com](mailto:bkalagotla@deloitte.com)<br/>
9441240562

