# Object.isSealed() #

## Definition ##
The Object.isSealed() method determines if an object is sealed.

## Need for this Standard ##
To determine whether the object is not extensible and removable.<br/>

    Object.isSealed(obj)

Returns true if the object is sealed, otherwise false. An object is sealed if it is not extensible and if all its properties are non-configurable and therefore not removable (but not necessarily non-writable).

## Usefulness of this standard ##

    // Objects aren't sealed by default.
    var empty = {};
    Object.isSealed(empty); // === false
    
    // If you make an empty object non-extensible, it is vacuously sealed.
    Object.preventExtensions(empty);
    Object.isSealed(empty); // === true
    
    // The same is not true of a non-empty object, unless its properties are all non-configurable.
    var hasProp = { fee: 'fie foe fum' };
    Object.preventExtensions(hasProp);
    Object.isSealed(hasProp); // === false
    
    // But make them all non-configurable and the object becomes sealed.
    Object.defineProperty(hasProp, 'fee', { configurable: false });
    Object.isSealed(hasProp); // === true
    
    // The easiest way to seal an object, of course, is Object.seal.
    var sealed = {};
    Object.seal(sealed);
    Object.isSealed(sealed); // === true
    
    // A sealed object is, by definition, non-extensible.
    Object.isExtensible(sealed); // === false
    
    // A sealed object might be frozen, but it doesn't have to be.
    Object.isFrozen(sealed); // === true (all properties also non-writable)
    
    var s2 = Object.seal({ p: 3 });
    Object.isFrozen(s2); // === false ('p' is still writable)
    
    var s3 = Object.seal({ get p() { return 0; } });
    Object.isFrozen(s3); // === true (only configurability matters for accessor properties)
    

## References ##
[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/isSealed](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/isSealed)


## Point of Contact ##
Bharath Kalagotla<br/>
[bkalagotla@deloitte.com](mailto:bkalagotla@deloitte.com)<br/>
9441240562

