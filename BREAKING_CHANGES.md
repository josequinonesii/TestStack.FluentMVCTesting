# Version 2.0.0

## ShouldRenderFileStream Method

The following overload of the `ShouldRenderFileStream` method has been *replaced*:

    public FileStreamResult ShouldRenderFileStream(string contentType = null)

We place emphasis on the word "replace" because it is important to note that this overload has not been removed but replaced - you will not encounter a compile-time error if you upgrade, but you will encounter a logical error when you run your existing test.

### Reason

The aforementioned overload has been replaced in order to enable an overload that takes a stream for comparison in a way that is consistent with the existing convention.

### Fix

Use a [named argument](http://msdn.microsoft.com/en-gb/library/dd264739.aspx).

As where you would have previously done this:

    ShouldRenderFileStream("application/json");
 
You must now do this: 

    ShouldRenderFileStream(contentType: "application/json");
    
    
## ShouldRenderFileMethod

The `ShouldRenderFile` method has been removed.

### Reason

The `ShouldRenderFile` method was ambiguous because it had the possibility to be interperted to test for a `FileResult` when in fact, it tested for a `FileContentResult`. 

It is for this reason that we introduced two unequivocal methods namely, `ShouldRenderAnyFile` and `ShouldRenderFileContents`.

### Fix

Use the `ShouldRenderFileContents` method instead: 

    ShouldRenderAnyFile()
    ShouldRenderAnyFile(contentType: "application/json")
    