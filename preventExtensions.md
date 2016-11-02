# Object.preventExtensions() #

## Definition ##
The *Object.preventExtensions()* method prevents new properties from ever being added to an object (i.e. prevents future extensions to the object).

## Need for this Standard ##
For preventing new properties being added to the object we can use this standard.<br/>

    Object.preventExtensions(obj)

*Object.preventExtensions()* marks an object as no longer extensible, so that it will never have properties beyond the ones it had at the time it was marked as non-extensible. Note that the properties of a non-extensible object, in general, may still be deleted. Attempting to add new properties to a non-extensible object will fail, either silently or by throwing a TypeError (most commonly, but not exclusively, when in strict mode).

## Usefulness of this standard ##
*Object.preventExtensions()* only prevents addition of own properties. Properties can still be added to the object prototype. However, calling Object.preventExtensions() on an object will also prevent extensions on its __proto__  property.

    // Object.preventExtensions returns the object being made non-extensible.
    var obj = {};
    var obj2 = Object.preventExtensions(obj);
    obj === obj2; // true
    
    // Objects are extensible by default.
    var empty = {};
    Object.isExtensible(empty); // === true
    
    // ...but that can be changed.
    Object.preventExtensions(empty);
    Object.isExtensible(empty); // === false
    
    // Object.defineProperty throws when adding a new property to a non-extensible object.
    var nonExtensible = { removable: true };
    Object.preventExtensions(nonExtensible);
    Object.defineProperty(nonExtensible, 'new', { value: 8675309 }); // throws a TypeError
    
    // In strict mode, attempting to add new properties to a non-extensible object throws a TypeError.
    function fail() {
      'use strict';
      nonExtensible.newProperty = 'FAIL'; // throws a TypeError
    }
    fail();
    
    // EXTENSION (only works in engines supporting __proto__
    // (which is deprecated. Use Object.getPrototypeOf instead)):
    // A non-extensible object's prototype is immutable.
    var fixed = Object.preventExtensions({});
    fixed.__proto__ = { oh: 'hai' }; // throws a TypeError
    

If there is a way to turn an extensible object to a non-extensible one, there is no way to do the opposite in ECMAScript 5.


## References ##
[https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/preventExtensions](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/preventExtensions)


## Point of Contact ##
Bharath Kalagotla<br/>
[bkalagotla@deloitte.com](mailto:bkalagotla@deloitte.com)<br/>
9441240562

