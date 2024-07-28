## Module 3. HTML5 File Upload and Download

Hi. This week, we will talk about the new version of Ajax called XHR2
for XMLHttpRequest Level 2 that plays an important role in today\'s
modern complex Web apps.

XHR2 introduces new capabilities like cross-origin requests, uploading
progress events, and support for uploading/downloading binary data.

You will learn how to download and upload files using XHR2, monitoring
the upload/download progress, etc.

The course will provide full examples of HTML5 forms that handle files
with client and server-side code provided. Drag'n'drop will be covered
as well, between elements inside an HTML document but also with files
from and to the desktop.

The second part of the week will show you how to use IndexedDB, a
powerful NoSQL database located in your browser, client side. Many
examples will be provided that will help you create, research, update
and delete data in that database.

We encourage you to use IndexedDB for saving and restoring the high
scores in the small game you have certainly wrote during week 2. Enjoy!

## 3.2.1 Ajax and XHR2

We present below a short history of Ajax: an introduction to
XMLHttpRequest level 2 (XHR2).

**Wikipedia definition**: *\"Ajax, short for Asynchronous JavaScript and
XML), is a group of interrelated Web development techniques used on the
client-side to create asynchronous Web applications. With Ajax, Web
applications can send data to and retrieve from a server asynchronously
(in the background) without interfering with the display and behavior of
the existing page. Data can be retrieved using
the XMLHttpRequest object. Despite the name, the use of XML is not
required (JSON is often used), and the requests do not need to be
asynchronous.\"*

Ajax appeared around 2005 with Google Maps, and is now widely used. We
are not going to teach you Ajax programming, but instead focus on the
relationships between \"the new version of Ajax\", known as XHR2 (for
XmlHttpRequest level 2) and the [File
API](https://www.w3.org/TR/FileAPI/) (seen in the W3Cx [HTML5 Coding
Essentials and Best
Practices](https://www.edx.org/course/html5-coding-essentials-and-best-practices) MOOC).
Also, you will discover that the HTML5 \<progress\> element is of great
use for monitoring the progress of file uploads (or downloads).

We recommend reading [this article from
HTML5Rocks.com](https://www.html5rocks.com/en/tutorials/file/xhr2/) that
presents the main features of XHR2.

Briefly, these improvements include:

-   New, easier to use syntax,

-   In-browser encoding/decoding of binary files,

-   Progress monitoring of uploads and downloads.

The following sections of this course present a few examples of file
downloads/uploads together with the file API and show how to monitor
progress.

The current support of XHR2 is excellent: see [related CanIUse\'s
browser compatibility table](https://caniuse.com/#feat=xhr2).

## 3.2.2 Ajax/XHR2 and binary files

Hi everyone! In this lesson, I will present you how we can manage file
uploads and file downloads with nice visualization of the progression.

In this example, I\'m downloading directly binary files into the browser
and as you will notice, we\'ve got some progression bars that move in
real time.

Earlier, before XHR2, the new version of Ajax, it was possible to do
this but we had to ask at regular intervals of time the cerver. « Hey
server! how many bytes did you receive from my Browser? » Now,
monitoring the progression is made much easier because we\'ve got
progression callbacks that are called by the browser while it\'s
uploading or downloading a file.

This small multitrack player I\'ve already shown during the week one,
about Web Audio, is downloading binary files, monitoring progress, and
so on.

Let\'s start with a very simple example.

Here I will download a song that is located on one of my servers
here\...

mainline.i3s.unice.fr

When I will click on the download (button) and play the example song, it
will start the download.

Let\'s look at the downloadSoundFile function, that is called when we
click on the button.

How do we use XHR2?

We first start by creating an object that is an XML HTTP request.

We set the method: GET is for downloading a file, the URL, and the last
parameter \"true\", leave it like that.

Then, as we are going to download a binary file, we set the response
type to

\"arrayBuffer\", and this is new. It was not possible with the previous
version of

Ajax, that was available in the browsers. HTTP is a text-based transfer
protocol.

The text encoded files needed to be decoded in the browser or in the
server.

And when we manually, programmatically, in the JavaScript code, used
Ajax, we had two decode this by hand.

Now, we ask the browser: \"please, decode this for me\" and give me
directly, automatically, a binary file.

We prepared the request here, then we send the request: xhr.send() will
send asynchronously the request.

That means that the server will handle this in the background.

This message \"Ajax request sent\...\", will be displayed as soon as
this instruction is executed.

And if the file we are going to download is big, is large, then it can
take from dozens of seconds, or maybe one minute.

And when the file is arrived the callback, xhr.onload callback, will be
called by the browser.

Then, we call the initSound() function that will decode in memory the
mp3 file, and then enable the start and stop buttons, so that we can
play the

song using Web Audio. Before looking at the initSound (function) let\'s
start it. I click...

You can see that the message \"Ajax request sent\" is displayed first,
then \"song downloaded\".

This is on the onload callback, and then we call the initSound function
that will decode the file and display the rest of the messages.

And now I can play the song.

In this example, we are using Web Audio: it\'s not streaming the sound.

It's playing a sample directly in memory so... you can give a look at
the code.

It uses what we saw during the first week.

The playSound function builds a small graph with the decoded buffer as a
source and directly to the speakers (to the destination).

If you want to monitor progress during download (so, this is the same
example), it\'s very easy.

Just use a progress HTML element with a value of zero, and it will grow
depending on the number of bytes the browser will have sent to the
remote server.

Or will have downloaded\... in case of a download.

When we started the request, we added a xhr.onprogress callback here
that gets in event sent by the browser, that has two properties.

One is called \"total\", that is a total number of bytes in the files we
are downloading, and \"loaded\" is the number of bytes we have actually downloaded.

And we can set these two properties directly to the \"value\" property
of the progress element and to the \"max\" property.

And if we try this (download the file), we can see the progress bar
growing because this onprogress callback is called regularly by the
browser every second or something like that.

It\'s very easy to monitor the progress.

You can put vertically this bar using CSS, change the style.

Refer to the HTML5 Part 1 course for that.

### Ajax and binary files - downloading files and monitoring progress

HTTP is a text-based protocol, so when you upload/download images,
videos or any binary file, they must first be text encoded for
transmission, then decoded on-the-fly upon receipt by the server or
browser. For a long time, when using Ajax, these binary files had to be
decoded \"by hand\", using JavaScript code. Not recommended!

We won\'t go into too much detail here, but all browsers (\> 2012)
support *XHR2*. XHR2 adds the option to directly download binary
data. With XHR2, you can ask the browser to encode/decode the file you
send/receive, natively. To do this, when you use XMLHttpRequest to send
or receive a file, you must set the xhr.responseType as arrayBuffer.

Below is a function that loads a sound sample using XMLHttpRequest level
2.

*Note*: 1) the simple and concise syntax, and 2) the use of the
new arrayBuffer type for the expected response (*line 5*):

```
1.  // Load a binary file from a URL as an ArrayBuffer.
2.  function loadSoundFile(url) {
3.  var xhr = new XMLHttpRequest();
4.  xhr.open(\'GET\', url, true);
5.  **xhr**.responseType = \'arraybuffer\';
6.  xhr.onload = function(e) {
7.  initSound(this.response); // this.response is an ArrayBuffer.
8.  };
9.  xhr.send();
10. }
```

#### Example: download a binary song file using XHR2 and responseType=\'arraybuffer\', and play it using Web Audio

[Try this example on
JSBin](https://jsbin.com/mecakaz/edit?html,js,console,output):

In this example, instead of reading the file from disk, we download it
using XHR2.

![Downloading file with
Xhr2](./images/image001.jpeg){width="5.0in"
height="2.484508967629046in"}

**Complete source code:**

```
1.  \<!DOCTYPE html\>
2.  \<html lang=\"en\"\>
3.   \<head\>
4.     \<title\>XHR2 and binary files + Web Audio API\</title\>
5.   \</head\>
6.  \<body\>
7.  \<p\>Example of using XHR2 and \<code\>xhr.responseType =
    \'arraybuffer\';\</code\> to download a binary sound file
8.  and start playing it on user-click using the Web Audio API.\</p\>
9.  
10. \<p\>
11. \<h2\>Load file using Ajax/XHR2 and the arrayBuffer response
    type\</h2\>
12. \<button **onclick=\"downloadSoundFile(\'https://myserver.com/song.mp3\');**\"\>
13.      Download and play example song.
14.  \</button\>
15. \<button onclick=\"playSound()\" disabled\>Start\</button\>
16. \<button onclick=\"stopSound()\" disabled\>Stop\</button\>
17. \<script\>
18.   // WebAudio context
19.   var context = new window.AudioContext();
20.   var source = null;
21.   var audioBuffer = null;
22.  
23.   function stopSound() {
24.     if (source) {
25.        source.stop();
26.     }
27.   }
28.  
29.   function playSound() {
30.     // Build a source node for the audio graph
31.     source = context.createBufferSource();
32.     source.buffer = audioBuffer;
33.     source.loop = false;
34.     // connect to the speakers
35.     source.connect(context.destination);
36.     source.start(0); // Play immediately.
37.   }
38.  
39.   function initSound(audioFile) {
40.     // The audio file may be an mp3 - we must decode it before playing it from memory
41.     context.decodeAudioData(audioFile, function(buffer) {
42.       console.log(\"Song decoded!\");
43.       // audioBuffer the decoded audio file we\'re going to work with
44.       audioBuffer = buffer;
45. 
46.       // Enable all buttons once the audio file is
47.       // decoded
48.       var buttons = document.querySelectorAll(\'button\');
49.       buttons\[1\].disabled = false; // play
50.       buttons\[2\].disabled = false; // stop
51.       alert(\"Binary file has been loaded and decoded, use play stop buttons!\")
52.     }, function(e) {
53.        console.log(\'Error decoding file\', e);
54.     });
55.   }
56.  
57.   // Load a binary file from a URL as an ArrayBuffer.
58.   function downloadSoundFile(url) {
59.     var xhr = new XMLHttpRequest();
60.     xhr.open(\'GET\', url, true);
61.  
62.     **xhr.responseType = \'arraybuffer\'; // THIS IS NEW WITH HTML5!**
63.     xhr.onload = function(e) {
64.        console.log(\"Song downloaded, decoding\...\");
65.        initSound(this.response); // this.response is an ArrayBuffer.
66.     };
67.     xhr.onerror = function(e) {
68.       console.log(\"error downloading file\");
69.     }
70.  
71.     xhr.send();
72.        console.log(\"Ajax request sent\... wait until it downloads completely\");
73.   }
74. \</script\>
75. \</body\>
76. \</html\>
```

**Explanations**: 

-   *Line 12*: a click on this button will call
    the downloadSoundFile function, passing it the URL of a sample mp3
    file.

-   *Lines 58-73*: this function sends the Ajax request, and when the
    file has arrived, the xhr.onload callback is called (*line 63*).

-   *Lines 39-55*: The initSound function decodes the mp3 into memory
    using the WebAudio API, and enables the play and stop buttons.

-   When the play button is enabled and clicked (*line 15*) it calls
    the playSound function. This builds a minimal Web Audio graph with
    a BufferSource node that contains the decoded sound (*lines 31-32*),
    connects it to the speakers (*line 35*), and then plays it.

### Monitoring uploads or downloads using a progress event

![downloading progression using a progress
element](./images/image002.jpeg){width="4.416666666666667in"
height="0.7916666666666666in"}

#### 1 - Declare a progress event handler

XHR2 now provides progress event attributes for monitoring data
transfers. Previous implementations of XmlHttpRequest didn\'t tell us
anything about how much data has been sent or received.
The [ProgressEvent](https://www.w3.org/TR/progress-events/) interface
adds 7 events relating to uploading or downloading files.

**attribute** | **type** | **Explanation**
|-------------|----------|------------------------------------------------------
| onloadstart | loadstart | When the request starts. |
| **onprogress** |  **progress** |  **While loading and sending data.** |
| onabort | abort | When the request has been aborted, either by |
|         |       | invoking the abort() method or navigating away |
|         |       | from the page. |
| onerror |  error | When the request has failed. |
| onload | load  | When the request has successfully completed. |
| ontimeout | timeout | When the author specified timeout has passed |
|           |         | before the request could complete. |
| onloadend | loadend | When the request has completed, regardless of |
|           |         | whether or not it was successful. |

The syntax for declaring progress event handlers is slightly different
depending on the type of operation: a download (using the GET HTTP
method), or an upload (using POST).

**Syntax for download:**

```
1.  var xhr = new XMLHttpRequest();
2.  xhr.open(\'GET\', url, true);
3.  \...
4.  xhr.onprogress = function(e) {
5.  // do something
6.  }
7.  xhr.send();
```

Note that an alternative syntax such
as xhr.addEventListener(\'progress\', callback, false) also works.

**Syntax for upload:**

```
1.  var xhr = new XMLHttpRequest();
2.  xhr.open(\'POST\', url, true);
3.  \...
4.  **xhr.upload.onprogress = function(e) {**
5.  **// do something**
6.  **}**
7.   
8.  xhr.send();
```

Notice that the only difference is the \"upload\" added after the name
of the request object: with GET we use xhr.onprogress and with POST we
use xhr.upload.onprogress.

Note that an alternative syntax such
as xhr.upload.addEventListener(\'progress\', callback, false) also
works.

#### 2 - Get progress values (how many bytes have been downloaded) and the total file size

The event e passed to the onprogress callback has two pertinent
properties:

1.  loaded which corresponds to the number of bytes that have been
    downloaded or uploaded by the browser, so far, and

2.  total which contains the file\'s size (in bytes).

Combining these with a \<progress\> element, makes it very easy to
render an animated *progress bar*. Here is a source code extract that
does this for a download operation:

HTML:

```
1.  \<progress id=\"downloadProgress\" value=0\>\<progress\>
```

### JavaScript:

```
1.  // progress element
2.  **var progress = document.querySelector(\'#downloadProgress\');**
3.   
4.  function downloadSoundFile(url) {
5.    var xhr = new XMLHttpRequest();
6.    xhr.open(\'GET\', url, true);
7.   
8.    \...
9.    xhr.onprogress = function(e) {
10.     **progress.value = e.loaded;**
11.     **progress.max = e.total;**
12.   }
13.   xhr.send();
14. }
```

**Explanations**: by setting the value and max attributes of
the \<progress\> element with the current number of bytes downloaded by
the browser and the total size of the file (*lines 10-11*), it will
reflect the actual proportions of the file downloaded/still to come.

For example, with a file that is 10,000 bytes long, if the current
number of bytes downloaded is 1000, then \<progress value=1000
max=10000\> will look like this: 

1.  ![progress bar
    10%](./images/image003.jpeg){width="2.6666666666666665in"
    height="0.5729166666666666in"}

And a current download of 2000 bytes will define \<progress value=2000
max=10000\> and will look like this:

2.  ![progress bar
    20%](./images/image004.jpeg){width="2.6666666666666665in"
    height="0.5in"}

### Complete example: monitoring the download of a song file

![monitoring download](./images/image005.jpeg){width="5.0in"
height="1.112713254593176in"}

This is a variant of the previous example that uses the progress event
and a \<progress\> HTML5 element to display an animated progression bar
while the download is going on.

[Try it on JSBin](https://jsbin.com/nuxanaf/edit?html,output) - look at
the code, which includes the previous source code extract.

## 3.2.3 Uploading files and monitoring progress

We saw how to download files. Let\'s see now how we can upload files!

Uploading a file means sending it to a remote server. In this example,
we will

just look at the simplest possible thing: uploading one single file.
Later on, in the course,

course you will see how to upload multiple files, including form input
fields and

so on. We\'ve got a file selector here: an input type=file, and we will
select one file.

For example, here I\'m selecting an mp3 song. As soon as the file has
been selected, in this example, you see that the file is uploaded to a
remote server.

Let\'s look at how we can get the file we selected and send it.

We attached to the file selector a change event listener, that will be
called as soon as we select the file. In this callback we create an XML
HTTP request and we indicate that it\'s a POST request.

POST is used for sending data to a remote server. We are using JSBin,
and the upload.html.

You see, here, is the URL of a fake server. We don\'t have a remote
server ready in this example, however JSBin handles that and pretends
that the server exists.

We created the request, indicated the method and the URL of the server.
Then, we will prepare an object that is a FormData object.

It\'s a container in which you can append files or append any sort of
data.

And the data are key/value pairs. Here I added an object called \"file\"
with a value that is the file I have selected earlier using the file
input type=file element.

And when I send the request, I pass the FormData object that contains
the file.

And then, as soon as the send method is called, the browser will handle
the upload in background.

And this may take some time.

Let\'s start again here\... if I select a file, you see that it takes
some time before it\'s uploaded.

And when the upload you see the \"upload complete message\" because when
the upload is complete the browser will call to onload callback for your
request.

And during the upload, it will call the xhr.upload.onprogress callback.

That\'s a function that works exactly like the xhr.onprogress callback
we used for downloading.

It\'s just this \".upload\" that you write before the \"onprogress\"
here. That\'s the only difference with monitoring progress with
download.

And here you can see that the \"upload complete\" message appears. If we
want to send multiple files, we can append multiple files here.

That\'s all for this video! Bye! Bye!

Here is an example that uses a FormData object for uploading one or more
files to an HTTP server.

Notice that the URL of the server is fake, so the request will fail.
However, the simulation takes time, and it is interesting to see how it
works.

Later on, we will show full examples of real working code with
server-side PHP source, during the "File API, drag and drop and XHR2"
lecture.

[Try the example on JSBin](https://jsbin.com/pidusap/edit):

![file upload example
1](./images/image006.jpeg){width="3.96875in"
height="2.21875in"}

### Source code of the example:

```
1.  \<!DOCTYPE html\>
2.  \<html lang=\"en\"\>
3.  \<head\>
4.     \<meta charset=\"utf-8\" /\>
5.     \<title\>File upload with XMLHttpRequest level 2 and HTML5\</title\>
6.  \</head\>
7.   
8.  \<body\>
9.  \<h1\>Example of XHR2 file upload\</h1\>
10.   Choose a file and wait a little until it is uploaded (on a fake  
11.   server). A message should pop up once the file is uploaded 100%.
12. \<p\>
13. \<input id=\"file\" type=\"file\" /\>
14. \</p\>
15. \<script\>
16. var fileInput = document.querySelector(\'#file\');
17.  
18. fileInput.onchange = function() {
19.    var xhr = new XMLHttpRequest();
20.    xhr.open(\'POST\', \'upload.html\'); // With FormData,
21.                                     // POST is mandatory
22.  

23.    **xhr.onload = function() {**

24.      **alert(\'Upload complete !\');**
25.    **};**
26.  
27.    **var form = new FormData();**
28.    **form.append(\'file\', fileInput.files\[0\]);**
29.    // send the request
30.    xhr.send(form);
31. };
32. \</script\>
33. \</body\>
34. \</html\>
```

### **Explanations**:

-   *Line 18*: callback called when the user selects a file.

-   *Lines 19-20*: preparation of the XHR2 request.

-   *Lines 27-30*: a FormData object is created (this will contain the
    (MIME) multipart form-data which will be sent by the POST request).

-   *Line 30:* the request is sent, with the FormData object passed as a
    parameter (all data is sent).

-   *Line 23*: when the file is completely uploaded, the onload listener
    is called and an alert message is displayed.

### Monitor the upload progress

Here is a more user-friendly example. It is basically the same, but this
time, we\'ll monitor the progress of the upload using a method similar
to that used for monitoring file downloads:

-   We use a \<progress\> element and its two attributes value and max.

-   We also bind an event handler to the progress event that an
    XMLHttpRequest will trigger. The event has two
    properties: loaded and total that respectively correspond to the
    number of bytes that have been uploaded, and to the total number of
    bytes we need to upload (i.e., the file size).

![file upload with progress
bar](./images/image007.jpeg){width="3.8958333333333335in"
height="1.28125in"}

Here is the code of such an event listener:

```
3.  xhr.upload.onprogress = function(e) {
4.    progress.value = e.loaded; // number of bytes uploaded
5.    progress.max = e.total;    // total number of bytes in the file
6.  };
```

### [Try the example on JSBin](https://jsbin.com/qedaja/edit?html,css,output):

### Code from this example (nearly the same as previous example\'s code):

```
1.  \<!DOCTYPE html\>
2.  \<html lang=\"en\"\>
3.  \<head\>
4.     \<meta charset=\"utf-8\" /\>
5.     \<title\>HTML5 file upload with monitoring\</title\>
6.  \</head\>
7.   
8.  \<body\>
9.  \<h1\>Example of XHR2 file upload, with progress bar\</h1\>
10. Choose a file and wait a little until it is uploaded (on a fake server).
11. \<p\>
12. \<input id=\"file\" type=\"file\" /\>
13. \<br/\>\<br/\>
14. **\<progress id=\"progress\" value=0\>\</progress\>**
15.  
16. \<script\>
17.    var fileInput = document.querySelector(\'#file\'),
18.    **progress = document.querySelector(\'#progress\');**
19.  
20.    fileInput.onchange = function() {
21.      var xhr = new XMLHttpRequest();
22.      xhr.open(\'POST\', \'upload.html\');
23.  
24.      **xhr.upload.onprogress = function(e) {**
25.        **progress.value = e.loaded;**
26.        **progress.max = e.total;**
27.      **};**
28. 
29.      xhr.onload = function() {
30.      alert(\'Upload complete!\');
31.    };
32.  
33.    var form = new FormData();
34.    form.append(\'file\', fileInput.files\[0\]);
35.  
36.    xhr.send(form);
37. };
38. \</script\>
39. \</body\>
40. \</html\>
```

The only difference between these two worked-examples is
the onprogress listener which updates the progress
bar\'s value and max attributes. 

## 3.2.4 Discussion and projects

Here is the discussion forum for this part of the course. Please either
post your comments/observations/questions or share your creations.

### Suggested topics of discussion:

-   Did you hear about [the Fetch API](https://davidwalsh.name/fetch)?
    This APIs  is easier to use than XhR2, but monitoring progress is a
    bit trickier and will require the use of the streams API. Monitoring
    upload is not yet supported. [See for example this
    article](https://javascript.info/fetch-progress).

-   Did you note that using XHR2 for monitoring progress is really
    simple and efficient?  What is your experience? Please share ;)

-   How can we monitor the speed of an upload/download in bytes per
    second? What would you propose? Did you find any interesting
    resources on the Web that explain that?

### Optional projects:

-   If you know how to program server-side code, please make a small app
    that will upload files, monitor the progress of the upload, save the
    files server-side, and send back a message containing the URLs of
    the files. Better: create a Web page that displays links to the
    uploaded files.

-   Try to write an assetLoader function that will download a set of
    images and sound (maybe using the BufferUtility seen during Module
    1), but this time with a progress bar. This could be useful for a
    game, or for a Web app that needs to load resources before starting.

## 3.3.1 Introduction

From [the W3C HTML 5.1
specification](https://www.w3.org/TR/html51/editing.html#dnd): *\"the
drag and drop API defines an event-based drag-and-drop mechanism, it
does not define exactly what a drag-and-drop operation actually is\"*.

We decided to present this API in a section about HTML5 client-side
persistence, as it is very often used for dragging and dropping files.
However, we will also address drag and drop of elements within an HTML
document.

We will start by presenting the API itself, and then we will focus on
the particular case of drag and dropping files.

### External resources

-   MDN article about [HTML Drag and Drop
    API](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API).

-   Medium article entitled \"[How to Drag & Drop HTML Elements and
    Files using
    Javascript](https://medium.com/@ralzohairi/how-to-drag-drop-html-elements-and-files-using-javascript-d31d15279369)\"

-   Nice [shopping cart
    demo](https://nettutsplus.s3.amazonaws.com/64_html5dragdrop/demo/index.html).

## 3.3.2 Drag detection

Hi! Welcome to the drag and drop lesson. So, the first thing is that
before looking at examples is that

you must know that not all elements in an HTML document are draggable

by default. By default, a text selection is draggable, as you can
see\... An image

is draggable too, but you cannot drag a H1 or drag a list item without
adding first a

draggable=true attribute.

In the examples we are going to detail. We added draggable=true to the
elements that will be candidate for drag and drop. Also, the first this
you must do, before doing anything, is to detect that an element has
been dragged. For this we are

using the ondragstartstart event listener, so either as an attribute
here, or in the

JavaScript. And, in that case we use a dragstart listener on the
numbered list, and children will inherit this event listener. This is
another particularity: you can define event listeners, for the drag and
drop on parents. And the children inherit this listener.

Let\'s look at a small example with drag and drop of list items. The
code we have

here on CodePen is the same as (the one) I\'ve just showed in the
course. We\'ve got a list with an ondragstart event handler, and we\'ve
got list items with draggable=true.

The code from the drastart handler is just showing an alert. If I click
and start to drag one item while maintaining the button pressed, it
displays a dragstart event. What we show here is that we display the
alert (the event.target), that means \"the element that raised, that
fired the event\". \".innerHTML », so it displays the content. Instead
of using \"innerHTML\" to get the HTML content here (the text inside the
list item), I can also use the dataset interface that is also an
addition from HTML5. And we can now add \"data attributes\" that start
with \"data\" followed by a minus sign, and this is the name of the data
attribute (\"value\"- in this case), so I can use the dataset interface
followed by the name of the attribute, and it will produce the same
thing: fruit-apple. And I can name it as I like: I can call it
\"data-fruit\" and, use it here\... and it works too. I can get the
content!

And these attributes, these data attributes, are all valid! I go back to
the initial code.

Once we managed to detect a drag, and can get some values\... some interesting values from the dragged
object, now we will detect a drop!

What do we do when we want to drag something and drop it somewhere, and
make something happen in the drop zone? We need to copy, in the
dragstart handler, some data that will be obtained back in the drop handler. There is a
clipboard called event.dataTransfer, that is specialized for drag and
drop. And it\'s got a setData method for writing in it a key/value pair,
so here we copy, with the name \"fruit\", the value of the data
attribute of the dragged object. And in the drop handler, we will get
back the data that was copied in the drag and drop clipboard, using
getData.

We wrote a value with a key=\"fruit\", we get this value back here. And
in the drop handler, in that case, we create a list item element and
then we initialize, we set the text content of the list item, with the value
corresponding to the value we got back from the clipboard.

And then, we just add to do drop zone\...
(#droppedFruits)\...appendChild() the list item. Let\'s look
at how the drop zone was defined: the drop zone in that
example is a div. We\'ve got an ondrop listener, that calls the drop
callback we just saw.

And we also added an ondragover=\"return false\" listener. This will
avoid the propagation of the event, because when we drag over
the drop zone, each mouse movement will fire a lot of dagover events and
this can slow down the browser\... so in that case we just returned
false for performance reasons. So, when I drop it, I\'m in the drop handler, I get
back \"Apples »,

I creates a list item, I set the list item content with \"Apples\", and
I append the list item to the drop,

to the div. That\'s all for this video! You understood the main steps
for doing drag and drop:

detect a drag, copy some data in the clipboard, detect a drop, get back
the data and do something. And avoid firing too many events by just stopping the
propagation with an ondragover=\"return false\";

See you for the next video! I will explain how to give a nice visual
feedback when we drag and drop things.

In order to make any visible element *draggable*, add
the draggable=\"true\" attribute to any visible HTML5 element. Notice
that some elements are draggable by default, such as \<img\> elements.

In order to detect a drag, add an event listener for
the dragstart event:

```
1.  \<ol **ondragstart=\"dragStartHandler(event)\"**\>
2.  \<li **draggable=\"true\"** data-value=\"fruit-apple\"\>Apples\</li\>
3.  \<li **draggable=\"true\"** data-value=\"fruit-orange\"\>Oranges\</li\>
4.  \<li **draggable=\"true\"** data-value=\"fruit-pear\"\>Pears\</li\>
5.  \</ol\>
```

In the above code, we made all of the \<li\> elements draggable, and we
detect a dragstart event occurring to any item within the ordered
list: \<ol ondragstart=\"dragStarthandler(event)\"\>.

> When you put an ondragstart handler on an element, each of its
> draggable children could fire the event! It\'s a sort of \"inheritance
> of handlers\"\... In the above example, the handler is declared at
> the \<ol\> level, so any subordinate \<li\> element will fire the
> event.

Try the following interactive example in your browser (just click and
drag one of the list items) or [play with it at
CodePen](https://codepen.io/w3devcampus/pen/MaWKZb).

### Screenshot:

![drag n drop fruits](./images/image008.jpeg){width="5.0in"
height="1.6084405074365704in"}

### Complete code from the example:

```
1.  \<!DOCTYPE html\>
2.  \<html lang=\"en\"\>
3.  \<head\>
4.     \<script\>
5.       function dragStartHandler(event) {
6.           alert(\'dragstart event, target:
     \' + event.target.innerHTML);
7.       }
8.   \</script\>
9.   \</head\>
10.  \<body\>
11.  \<p\>What fruits do you like? Try to drag an element!\</p\>
12.  \<ol ondragstart=\"dragStartHandler(event)\"\>
13.  \<li draggable=\"true\" data-value=\"fruit-apple\"\>Apples\</li\>
14.  \<li draggable=\"true\" data-value=\"fruit-orange\"\>Oranges\</li\>
15.  \<li draggable=\"true\" data-value=\"fruit-pear\"\>Pears\</li\>
16.  \</ol\>
17. \<p\>Drop your favorite fruits below:\</p\>
18.  \<body\>
19. \<html\>
```

In this script, the event handler will only display an alert showing the
name of the target element that launched the event. 

## 3.3.3 Drop detection

Let\'s continue to develop the example. We show how to drag an element
and detect a drop, receiving a value which corresponds to the dragged
element. Then we change the page content accordingly.

#### Step #1: in the dragstart handler, copy a value in the drag and drop clipboard for later use

When a draggable \<li\> element is being dragged, in
the dragstart handler [get the value of its data-value
attribute](https://html5doctor.com/html5-custom-data-attributes/) and
copy it to *the \"drag and drop clipboard\" *for later use.

When data is copied to this clipboard, a key/value pair must be given.
The data copied to the clipboard is associated with this name.

The variable event.target at *line 5* below is the \<li\> element that
has been dragged, and event.target.dataset.value is the value of its
data-value attribute (in our case \"apples\", \"oranges\" or \"pears\"):

```
1.  function dragStartHandler(event) {
2.      console.log(\'dragstart event, target:
    \' + event.target.innerHTML);
3.  
4.      // Copy to the drag\'n\'drop clipboard the value of the
5.      // data\* attribute of the target,
6.      // with a type \"Fruit\".
7.   **event.dataTransfer.setData(\"Fruit\", event.target.dataset.value);**
8.  }
```

#### Step #2: define a \"drop zone\"

Any visible HTML element may become a \"drop zone\"; if we attach an
event listener for the drop event. Note that most of the time, as events
may be propagated, we will also listen for dragover or dragend events
and stop their propagation. More on this later\...

```
1.  \<div **ondragover=\"return false\"** **ondrop=\"dropHandler(event);**\"\>
2.  Drop your favorite fruits below:
3.  \<ol id=\"droppedFruits\"\>\</ol\>
4.  \</div\>
```

Whenever the mouse is moving above a (any) drop zone, dragover events
will fire. Accordingly, a large number of dragover events may need to be
handled before the element is finally dropped. The ondragover handler is
used to avoid propagating dragover events. This is done by returning
the false value at *line 1*.

#### Step #3: write a drop handler, fetch content from the clipboard, and do something with it

```
1.  function dropHandler(event) {
2.     console.log(\'drop event, target: \' + event.target.innerHTML);
3.  
4.     \...
5.  
6.     // get the data from the drag\'n\'drop clipboard,GET
7.     // with a type=\"Fruit\"
8.     var data = event.dataTransfer.getData(\"Fruit\");
9.  
10.    // do something with the data
11.    \...
12. }
```

Typically, in the drop handler, we need to acquire data about the
element that has been dropped (we get this from the clipboard at *lines
6-8,* the data was copied there during step 1 in the dragstart handler).

### Complete example

![drag n drop
fruits](./images/image09.jpeg){width="3.90625in"
height="3.2291666666666665in"}

### Try it in your browser below or [play with it at CodePen](https://codepen.io/w3devcampus/pen/YyzWKy?editors=110):

### Source code:

```
1.  \<!DOCTYPE html\>
2.  \<html\>
3.  \<head\>
4.     \<script\>
5.        function dragStartHandler(event) {
6.            console.log(\'dragstart event, target: \' +
7.                         event.target.innerHTML);
8.            // Copy to the drag\'n\'drop clipboard the value
9.            // of the data\* attribute of
10.           // the target, with a type \"Fruits\".
11.           event.dataTransfer.setData(\"Fruit\",
12.                                 event.target.dataset.value);
13.       }
14. 
15.       function dropHandler(event) {
16.          console.log(\'drop event, target: \' +
17.                                 event.target.innerHTML);
18.          var li = document.createElement(\'li\');
19.          // get the data from the drag\'n\'drop clipboard,
20.          // with a type=\"Fruit\"
21.          var data = event.dataTransfer.getData(\"Fruit\");
22. 
23.          if (data == \'fruit-apple\') {
24.             li.textContent = \'Apples\';
25.          } else if (data == \'fruit-orange\') {
26.             li.textContent = \'Oranges\';
27.          } else if (data == \'fruit-pear\') {
28.             li.textContent = \'Pears\';
29.          } else {
30.             li.textContent = \'Unknown Fruit\';
31.          }
32.          // add the dropped data as a child of the list.
33.          document.querySelector(\"#droppedFruits\").appendChild(li);
34.       }
35.   \</script\>
36. \</head\>
37. \<body\>
38.    \<p\>What fruits do you like? Try to drag an element!\</p\>
39.    \<ol ondragstart=\"dragStartHandler(event)\"\>
40.    
     \<li draggable=\"true\" data-value=\"fruit-apple\"\>Apples\</li\>
41.    
     \<li draggable=\"true\" data-value=\"fruit-orange\"\>Oranges\</li\>
42.    
      \<li draggable=\"true\" data-value=\"fruit-pear\"\>Pears\</li\>
43.    \</ol\>
44.  
     \<div ondragover=\"return false\" ondrop=\"dropHandler(event);\"\>
45.        Drop your favorite fruits below:
46.        \<ol id=\"droppedFruits\"\>\</ol\>
47.    \</div\>
48. \<body\>
49. \<html\>
```

### In the above code, note:

-   *Line 44*: we define the drop zone (ondrop=\...), and when a drag
    enters the zone we prevent event propagation (ondragover=\"return
    false\")

-   When we enter the dragstart listener (*line 5*), we copy the
    dragged-element\'s data-value attribute to the drag and
    drop clipboard with a name/key equal to \"Fruit\" (*line 11*),

-   When a drop occurs in the \"drop zone\" (the \<div\> at *line 44*),
    the dropHandler(event) function is called. This always occurs after
    a call to the dragstart handler. In other words: when we enter
    the drop handler, there must always be something on the clipboard!
    We use an event.dataTransfer.setData(\...) in the dragstart handler,
    and an event.dataTransfer.getData(\...) in the drop handler.

-   The dropHandler function is called (*line 15*), we get the
    object with a name/key equal to \"Fruit\" (*line 21*) from the
    clipboard , we create a \<li\> element (*line 18*), and set its
    value according to the value in that clipboard object (*lines
    23-31*),

-   Finally we add the \<li\> element to the \<ol\> list within the drop
    zone \<div\>.

Notice that we use some CSS to set aside some screen-space for the drop
zone (not presented in the source code above, but available in the
online example):

```
1.  div {
2.     height: 150px;
3.     width: 150px;
4.     float: left;
5.     border: 2px solid #666666;
6.     background-color: #ccc;
7.     margin-right: 5px;
8.     border-radius: 10px;
9.     box-shadow: inset 0 0 3px #000;
10.    text-align: center;
11.    cursor: move;
12. }
13. 
14. li:hover {
15.    border: 2px dashed #000;
16. }
```

## 3.3.4 A few words about data-\* attributes

Microdata is a powerful way to add structured data into HTML code, but
HTML5 has also added the possibility of adding arbitrary data to an HTML
element. For example, adding an attribute to specify the name of the
photographer (or painter?) of a picture, or any kind of information that
does not be fit within the regular attributes of the \<img\> element,
like alt.

Suppose you coded: **\<img src=\"photo.jpg\" photographer=\"Michel
Buffa\" date=\"14July2020\"\>**? It would **not** be valid!

However, with HTML5 we may add attributes that start with data- followed
by any string literal (WITH NO UPPERCASE) and it will be treated as
a storage area for private data. This can later be accessed in your
JavaScript code.

Valid HTML5 code: **\<img src=\"photo.jpg\" data-photographer=\"Michel
Buffa\" date=\"14July2020\"\>**. You can set the data- attribute to any
value.

The reason for this addition is that, in a bid to keep the HTML code
valid, some classic attributes like alt, rel and title have often been
misused for storing arbitrary data. The data-\*attributes of HTML5 are
an \"official\" way to add arbitrary data to HTML elements that is also
valid HTML code.

The specification says: \"Custom data attributes are intended to store
custom data private to the page or application, for which there are no
more appropriate attributes or elements.\"

**Data attributes are meant to be used by JavaScript and eventually by
CSS rules: embed initial values for some data, or use data- attributes
instead of JavaScript variables for easier CSS mapping, etc.**

### JavaScript API: the dataset property

Data attributes can be created and accessed using the dataset property
of any HTML element.

Here is [an online at
JsBin](https://jsbin.com/yowimebawo/edit?html,css,js,output) example: 

![Data attribut example
1](./images/image010.png){width="5.0in"
height="0.8055555555555556in"}

In this example, when you click on the sentence that starts with \"John
Says\", the end of the sentence changes, and the values displayed
are taken from data­-\* attributes of the \<li\> element.

### HTML code from the example:

```
1.  \<li class=\"user\" **data-name=\"John
    Resig\"** **data-city=\"Boston\"**
2.      **data-lang=\"js\"** **data-food=\"Bacon\"**\>
3.  \<b\>John says:\</b\> \<span\>Hello, how are you?\</span\>
4.  \</li\>
```

We just defined four data‐ attributes. 

### JavaScript code from the example:

```
1.  \<script\>
2.    var user = document.getElementsByTagName(\"li\")\[0\];
3.    var pos = 0, span = user.getElementsByTagName(\"span\")\[0\];
4.    var phrases = \[
5.      {name: \"city\", prefix: \"I am from \"},
6.      {name: \"food\", prefix: \"I like to eat \"},
7.      {name: \"lang\", prefix: \"I like to program in \"}
8.    \];
9.    user.addEventListener( \"click\", function(){
10.     // Pick the first, second or third phrase
11.     var phrase = phrases\[ pos++ % 3 \];
12. 
13.     // Use the .dataset property depending on the value of
    phrase.name
14.     // phrase.name is \"city\", \"food\" or \"lang\"
15.     span.innerHTML = phrase.prefix + user.dataset\[ phrase.name \];
16. 
17.     // could be replaces by old way..
18.     // span.innerHTML = phrase.prefix +
    user.getAttribute(\"data-\" + phrase.name );
19.   }, false);
20. \</script\>
```

All data‐ attributes are accessed using the dataset property of the HTML
element: in this example, user.dataset\[phrase.name\] is
either user.dataset.city, user.dataset.food, or user.dataset.lang.

### Using CSS pseudo elements ::before and ::after with the attr() function to display the value of data-\* attributes

This example shows how data-\* attributes can be added on the fly by
JavaScript code and accessed from a CSS rule using
the attr() CSS function.

Try [the online example at JsBin](https://jsbin.com/alunuk/6/edit). 

![Using CSS attr()
function](./images/image011.png){width="3.1770833333333335in"
height="0.8541666666666666in"}

### HTML code from this example:

```
1.  \<input type=\"range\" min=\"0\" max=\"100\" value=\"25\"\>
```

This is just one of the new input types introduced by HTML5.

### JavaScript code from this example:

```
1.  \<script\>
2.  var input = document.querySelector(\'input\');
3.   
4.  input.dataset.myvaluename = input.value; // Set an initial value.
5.   
6.  input.addEventListener(\'change\', function(e) {
7.      this.dataset.myvaluename = this.value;
8.  });
9.  \</script\>
```

### CSS code from this example:

```
1.  \<style\>
2.  input::after {
3.      color:red;
4.      content:** attr(data-myvaluename)** \'/\' attr(max);
5.      position: relative;
6.      left: 100px; top: -15px;
7.  }
8.  \</style\>
```

The attr() function takes an attribute name as a parameter and returns
its value. Here we used the name of the attribute we added on the fly.

## 3.3.5 Add visual feedback

Hi! Let\'s add some visual feedback to the drag and drop operations.

In this example, you can see that when we drag elements, the look and
feel is green with a dashed border around the dragged element.

And when I enter the drop zone, or drag over the drop zone, you can see
different things: first, the drop zone is affected: it becomes green
with a dashed border and also you get a \"+\" sign that appears, you see
this? These are things you can configure. The way we do that, is that we
added to the drop zone a 'dragenter' event listener, a 'dragleave' event
listener, a 'dragover' event listener. \"enter\" and \"leave\" are
straightforward, and the 'dragover' listener is for stopping the
propagation of the event.

I explained in the previous video that it\'s good for performance
reasons.

On the 'dragstart' handler, when we start to drag the element, we will
copy the data we need to get back once we dropped the elements, but we
will also change some of the style (the CSS style) of the dragged
element. And to remove this style, we also listen to the 'dragend'
event. Let\'s have a look at the CSS. In the CSS, we defined two
classes:

one is called \"dragged\" and the other \"draggedOver\". I just
discovered that they are

the same... so there is certainly a way to simplify this example\... So,
the \"dragged\" and the \"draggedOver\" classes just add a border (2
pixels dashed black)

and change the background color to green.

Let\'s have a look at the JavaScript: let\'s look at the 'dragenter',
the 'dropleave' and the 'dropenter' handlers. What do we do when we
enter the drop zone?

When we enter the drop zone, we use the classList interface, that was
also an HTML5 addition, and with this classList interface you can remove
CSS classes or add CSS classes.

When we enter the drop zone, we add, to the element we entered, the
\"draggedOver\" CSS class, that corresponds to a border and a background
color.

This is how, when I enter the drop zone, the div becomes green. And when
I leave (this is a 'dragleave' handler), that will remove the class. And
the same with the the dragstart handler.

When I start to drag an element, I add the class here. And I exaggerate the opacity,
the transparency, by setting a higher value for the opacity. Because
when you drag and drop elements, they are a bit lighter than normal, and here we accentuate
this effect. We can go further by
using some properties called the \"dropEffect\" and the \"allowEffect\"
properties. So in that case, when we start moving here, we can change the cursor and the \"+\" sign that you see here, can be
also customized by setting the dropEffect property in the 'dropenter listener'. Let\'s look at how we can do that: in the
'dragstart' listener, here\... in the dragStartHandler, we create an image, we set
it to a source, we give it a width, and we use the dataTransfert.setDragImage(dragIcon). This is the name of
the image I created (it\'s the HTML5 logo).

We can also proposes an offset relative to the cursor, the mouse cursor.
When I enter (in the dragEnterHandler), by setting the dropEffect property of the dataTransfer object, it
produces a \"+\" sign. You can use different values for the allowEffect
and dropEffect, that I explained in the course for producing small icons similar to the
ones you\'ve got on Windows when making shortcuts or just moving a file from
one folder to another. Bye bye!

### Add visual feedback when you drag something, when the mouse enters a drop zone, etc.

We can associate some CSS styling with the lifecycle of a drag and drop.
This is easy to do as the drag and drop API provides many events we can
listen to, and can be used on the draggable elements as well as in the
drop zones:

-   **dragstart**: this event, which we discussed in a previous
    section, is used on draggable elements. We used it to get a value
    from the element that was dragged, and copied it onto the clipboard.
    It\'s a good time to add some visual feedback - for example, by
    adding a CSS class to the draggable object.

-   **dragend**: this event is launched when the drag has ended (on a
    drop or if the user releases the mouse button outside a drop zone).
    In both cases, it is a best practice to reset the style of the
    draggable object to default.

The next screenshot shows the use of CSS styles (green background +
dashed border) triggered by the start of a drag operation. As soon as
the drag ends and the element is dropped, we reset the style of the
dragged object to its default. The full runnable online example is a bit
further down the page (it includes, in addition, visual feedback on the
drop zone):

![drag n drop
colorful](./images/image012.jpeg){width="5.0in"
height="2.577457349081365in"}

### Source code extract:

```
1.  \...
2.  \<style\>
3.    .dragged {
4.       border: 2px dashed #000;
5.       background-color: green;
6.    }
7.  \</style\>
8.  \<script\>
9.    function dragStartHandler(event) {
10.      **// Change CSS class for visual feedback**
11.      event.target.style.opacity = \'0.4\';
12.      event.target.**classList**.add(\'dragged\');
13. 
14.      console.log(\'dragstart event, target: \' + event.target);
15.      // Copy to the drag\'n\'drop clipboard the value of the data\*
   attribute of the target,
16.      // with a type \"Fruits\".
17.    
     event.dataTransfer.setData(\"Fruit\", event.target.dataset.value);
18.   }
19. 
20.   function dragEndHandler(event) {
21.      console.log(\"drag end\");
22.      **// Set draggable object to default style**
23.      event.target.style.opacity = \'1\';
24.      event.target.classList.remove(\'dragged\');
25.   }
26. \</script\>
27. \...
28. \<ol
    ondragstart=\"dragStartHandler(event)\" ondragend=\"dragEndHandler(event)\" \>
29.     \<li
    draggable=\"true\" data-value=\"fruit-apple\"\>Apples\</li\>
30.     \<li
    draggable=\"true\" data-value=\"fruit-orange\"\>Oranges\</li\>
31.     \<li draggable=\"true\" data-value=\"fruit-pear\"\>Pears\</li\>
32. \</ol\>
```

Notice at *lines 12 and 24* the use of the classlist property that has
been introduced with HTML5 in order to allow CSS class manipulation from
JavaScript.

### Other events can also be handled:

-   **dragenter**: usually we bind this event to the drop zone. The
    event occurs when a dragged object enters a drop zone. So, we could
    change the look of the drop zone.

-   **dragleave**: this event is also used in relation to the drop zone.
    When a dragged element leaves the drop zone (maybe the user changed
    his mind?), we must set the look of the drop zone back to normal.

-   **dragover**: this event is also generally bound to elements that
    correspond to a drop zone. A best practice here is to prevent the
    propagation of the event, and also to prevent the default behavior
    of the browser (i.e. if we drop an image, the default behavior is to
    display its full size in a new page, etc.)

-   **drop**: also on the drop zone. This is when we actually process
    the drop (get the value from the clipboard, etc). It\'s also
    necessary to reset the look of the drop zone to default.

#### Complete example with visual feedback on draggable objects and the drop zone

The following example shows how to use these events in a droppable
zone. 

Try it in your browser below or [directly at
CodePen](https://codepen.io/w3devcampus/pen/ojNLEL):

Complete source code (for clarity\'s sake, we put the CSS and JavaScript
into a single HTML page):

```
1.  \<!DOCTYPE html\>
2.  \<html\>
3.  \<head\>
4.     \<style\>
5.       div {
6.          height: 150px;
7.          width: 150px;
8.          float: left;
9.          border: 2px solid #666666;
10.         background-color: #ccc;
11.         margin-right: 5px;
12.         border-radius: 10px;
13.         box-shadow: inset 0 0 3px #000;
14.         text-align: center;
15.         cursor: move;
16.      }
17. 
18.      .dragged {
19.         border: 2px dashed #000;
20.         background-color: green;
21.      }
22. 
23.      .draggedOver {
24.         border: 2px dashed #000;
25.         background-color: green;
26.      }
27. \</style\>
28. \<script\>
29.      function dragStartHandler(event) {
30.         // Change css class for visual feedback
31.         event.target.style.opacity = \'0.4\';
32.         event.target.classList.add(\'dragged\');
33. 
34.         console.log(\'dragstart event, target:
    \' + event.target.innerHTML);
35.         // Copy in the drag\'n\'drop clipboard the value of the
    data\* attribute of the target,
36.         // with a type \"Fruits\".
37.        
    event.dataTransfer.setData(\"Fruit\", event.target.dataset.value);
38.      }
39. 
40.      function dragEndHandler(event) {
41.         console.log(\"drag end\");
42.         event.target.style.opacity = \'1\';
43.         event.target.classList.remove(\'dragged\');
44.      }
45. 
46.      function dragLeaveHandler(event) {
47.         console.log(\"drag leave\");
48.         event.target.classList.remove(\'draggedOver\');
49.      }
50. 
51.      function dragEnterHandler(event) {
52.         console.log(\"Drag enter\");
53.         event.target.classList.add(\'draggedOver\');
54.      }
55. 
56.      function dragOverHandler(event) {
57.         //console.log(\"Drag over a droppable zone\");
58.         event.preventDefault(); // Necessary. Allows us to drop.
59.      }
60. 
61.      function dropHandler(event) {
62.         console.log(\'drop event, target: \' + event.target);
63.         // reset the visual look of the drop zone to default
64.         event.target.classList.remove(\'draggedOver\');
65. 
66.         var li = document.createElement(\'li\');
67.         // get the data from the drag\'n\'drop clipboard, with a
    type=\"Fruit\"
68.         var data = event.dataTransfer.getData(\"Fruit\");
69. 
70.         if (data == \'fruit-apple\') {
71.             li.textContent = \'Apples\';
72.         } else if (data == \'fruit-orange\') {
73.             li.textContent = \'Oranges\';
74.         } else if (data == \'fruit-pear\') {
75.             li.textContent = \'Pears\';
76.         } else {
77.             li.textContent = \'Unknown Fruit\';
78.      }
79.      // add the dropped data as a child of the list.
80.      document.querySelector(\"#droppedFruits\").appendChild(li);
81.    }
82.   \</script\>
83. \</head\>
84. \<body\>
85. \<p\>What fruits do you like? Try to drag an element!\</p\>
86. \<ol ondragstart=\"dragStartHandler(event)\" ondragend=\"dragEndHandler(event)\" \>
87.  
      \<li draggable=\"true\" data-value=\"fruit-apple\"\>Apples\</li\>
88.  
      \<li draggable=\"true\" data-value=\"fruit-orange\"\>Oranges\</li\>
89.     \<li draggable=\"true\" data-value=\"fruit-pear\"\>Pears\</li\>
90. \</ol\>
91. \<div id=\"droppableZone\" ondragenter=\"dragEnterHandler(event)\" ondrop=\"dropHandler(event)\"
92.    
     ondragover=\"dragOverHandler(event)\" ondragleave=\"dragLeaveHandler(event)\"\>
93.       Drop your favorite fruits below:
94.       \<ol id=\"droppedFruits\"\>\</ol\>
95.  \</div\>
96. \<body\>
97. \<html\>
```

## 3.3.6 The dropEffect property

### More feedback using the dropEffect property: changing the cursor\'s shape

It is possible to change the cursor\'s shape during the drag process.
The cursor will turn into a \"copy\", \"move\" or \"link\" icon,
depending on the semantic of your drag and drop, when you enter a drop
zone during a drag. For example, if you \"copy\" a fruit into the drop
zone, as we did in the previous example, a \"copy\" cursor like the one
below would be appropriate:

![dropEffect](./images/image013.jpeg){width="2.3958333333333335in"
height="0.78125in"}

If you are \"moving\" objects, this style of cursor would be
appropriate:

![drop effect
#2](./images/image014.jpeg){width="2.5833333333333335in"
height="0.8854166666666666in"}

And if you are making a \"link\" or a \"shortcut\", a cursor would be
looking like this:

![drop effect #3](./images/image015.jpeg){width="2.65625in"
height="0.9375in"}

Alternatively, you could use any custom image/icon you like:

![drop effect with
image](./images/image016.jpeg){width="5.135416666666667in"
height="4.354166666666667in"}

To give this visual feedback, we use
the effectAllowed and dropEffect properties of the dataTransfer object.
To set one of the possible predefined cursors, we specify an effect in
the dragstart handler, and we set the effect (to \"move\", \"copy\",
etc.) in the dragEnter or dragOver handler.

Here is an extract of the code we can add to the example we saw earlier:

1.  function dragStartHandler(event) {

2.      **// Allow a \"copy\" cursor effect**

3.      **event.dataTransfer.effectAllowed = \'copy\';**

4.      \...

5.  }

And here is where we can set the cursor to a permitted value:

1.  function dragEnterHandler(event) {

2.     **// change the cursor shape to a \"+\"**

3.     **event.dataTransfer.dropEffect = \'copy\';**

4.     \...

5.  }

To set a custom image, we also do the following in
the dragstart handler:

1.  function dragStartHandler(event) {

2.     // allowed cursor effects

3.     event.dataTransfer.effectAllowed = \'copy\';

4.  

5.     **// Load and create an image**

6.     var dragIcon = document.createElement(\'img\');

7.     dragIcon.src = \'anImage.png\';

8.     dragIcon.width = 100;

9.  

10.    **// set the cursor to this image, with an offset in X, Y**

11.    **event.dataTransfer.setDragImage(dragIcon, -10, -10);**

12.    \...

13. }

### Complete online example

Here is the previous example (with apples, oranges, etc) that sets a
\"copy\" cursor and a custom image. Try it in your browser below (start
to drag and wait a few seconds for the image to be loaded. You might
have to try twice before it works) or [play with it at
CodePen](https://codepen.io/w3devcampus/pen/ZbEpEE):

Here are the various possible values for cursor states (your browser
will not necessarily support all of these; we noticed that copyMove,
etc. had no effect with Chrome, for example). The values of \"move\",
\"copy\", and \"link\" are widely supported.

All possible values for dropEffect and effectAllowed:

-   **dataTransfer.effectAllowed** can be set to the following
    values: none, copy, copyLink, copyMove, link, linkMove, move, all,
    and uninitialized.

-   **dataTransfer.dropEffect **can take on one of the following
    values: **none**, **copy**, **link**, **move**.

## 3.3.7 Drag and drop HTML elements

### Drag and drop images or any HTML element within a document

We saw the main principles of HTML5 drag and drop in the previous
sections. There are other interesting uses that differ in the way we
copy and paste things to/from the clipboard. The clipboard is accessed
through the dataTransfer property of the different events:

1.  event.dataTransfer.setData(\"Fruit\", event.target.dataset.value);

2.  \...

3.  var data = event.dataTransfer.getData(\"Fruit\");

#### \<img\> elements are all draggable by default!

Normally, to make an element draggable, you must add
the draggable=true attribute. \<img\> elements are an exception: they
are draggable by default! The next example shows how to drag and drop an
image from one location in the document to another.

#### Example: move images as an HTML subtree

Try this example (adapted
from [braincracking.org](https://web.archive.org/web/20160219080616/http:/html5demo.braincracking.org/demo/dragNDrop.php) (in
French)) in your browser below or [play with it at
CodePen](https://codepen.io/w3devcampus/pen/xwxEZg):

Code from the example:

1.  \<html lang=\"en\"\>

2.  \<head\>

3.  \<style\>

4.     .box {

5.        border: silver solid;

6.        width: 256px;

7.        height: 128px;

8.        margin: 10px;

9.        padding: 5px;

10.       float: left;

11.    }

12. \</style\>

13. \<script\>

14.     function drag(target, evt) {

15.         evt.dataTransfer.setData(\"Text\", target.id);

16.     }

17.     function drop(target, evt) {

18.         var id = evt.dataTransfer.getData(\"Text\");

19.         target.appendChild(document.getElementById(id));

20.         // prevent default behavior

21.         evt.preventDefault();

22.     }

23. \</script\>

24. \</head\>

25. \<body\>

26. Drag and drop browser images in a zone:\<br/\>

27.  
     \<img src=\"https://mainline.i3s.unice.fr/mooc/ABiBCwZ.png\" id=\"cr\" 
        

28.         ondragstart=\"drag(this, event)\" alt=\"Logo Chrome\"\>

29.  
     \<img src=\"https://mainline.i3s.unice.fr/mooc/n7xo93U.png\" id=\"ff\"

30.         ondragstart=\"drag(this, event)\" alt=\"Logo Firefox\"\>

31.  
     \<img src=\"https://mainline.i3s.unice.fr/mooc/ugUmuGQ.png\" id=\"ie\"

32.         ondragstart=\"drag(this, event)\" alt=\"Logo IE\"\>

33.  
     \<img src=\"https://mainline.i3s.unice.fr/mooc/jfrNErz.png\" id=\"op\"

34.         ondragstart=\"drag(this, event)\" alt=\"Logo Opera\"\>

35.  
     \<img src=\"https://mainline.i3s.unice.fr/mooc/gDJCG0l.png\" id=\"sf\"

36.         ondragstart=\"drag(this, event)\" alt=\"Logo
    Safari\"\>\<br/\>

37. 

38.  
     \<div class=\"box\" ondragover=\"return false\" ondrop=\"drop(this, event)\"\>

39.         \<p\>Good web browsers\</p\>

40.    \</div\>

41.  
     \<div class=\"box\" ondragover=\"return false\" ondrop=\"drop(this, event)\"\>

42.         \<p\>Bad web browsers\</p\>

43.    \</div\>

44. \</body\>

45. \</html\>

The trick here is to only work on the DOM directly. We used a variant of
the event handler proposed by the DOM API. This time, we used handlers
with two parameters (the first parameter, target, is the element that
triggered the event, and the second parameter is the event itself). In
the dragstart handler we copy just the id of the element in the DOM
(*line 15*).

In the drop handler, we just move the element from one part of the DOM
tree to another (under the \<div\> defined at *line 38*, that is the
drop zone). This occurs at *line 18* (get back the id from the
clipboard), and *line 19* (make it a child of the div. Consequently, it
is no longer a child of the \<body\>, and indeed we have \"moved\"
one \<img\> from its initial position to another location in the page).

## 3.3.8 Drag and drop a text selection

![](./images/image017.png){width="5.0in"
height="1.7537390638670167in"}

**There is no need to add a dragstart handler on an element that
contains text.** Any selected text is automatically added to the
clipboard with a name/key equal to \"text/plain\". Just add a drop event
handler on the drop zone and fetch the data from the clipboard using
\"text/plain\" as the access key:

1.  function drop(target, event) {

2.     event.preventDefault();

3.   
     target.innerHTML = event.dataTransfer.getData(**\'text/plain\'**);

4.  };

#### Example: select some text and drag and drop the selection in the drop zone

Try it in your browser below (select text, then drag and drop it into
the drop zone) or [play with it at
CodePen](https://codepen.io/w3devcampus/pen/vNYXyR):

Complete source code from the example:

1.  \<html lang=\"en\"\>

2.  \<head\>

3.  \<style\>

4.     .box {

5.        border: silver solid;

6.        width: 256px;

7.        height: 128px;

8.        margin: 10px;

9.        padding: 5px;

10.       float: left;

11.    }

12. 

13.    .notDraggable {

14.       user-select: none;

15.    }

16. \</style\>

17. \<script\>

18.     function drop(target, event) {

19.        event.preventDefault();

20.      
     target.innerHTML = event.dataTransfer.getData(\'text/plain\');

21.     };

22. \</script\>

23. \</head\>

24. \<body\>

25. \<p id=\"text\"\>

26.     \<b\>Drag and drop a text selection from this paragraph\</b\>.
    Drag and drop any

27.     part of this text to

28.     the drop zone. Notice in the code: there is no need for a
    dragstart handler in case of

29.     text selection:

30.     the text is added to the clipboard when dragged with a key/name
    equal to \"text/plain\".

31.     Just write a

32.     drop handler that will do an
    event.dataTransfer.getData(\"text/plain\") and you are

33.     done!

34.  \</p\>

35. 

36. **\<p class=\"notDraggable\"\>**

37.      This paragraph is not selectable however. Look at the CSS in
    the source code.

38. \</p\>

39. 

40. \<div class=\"box\" ondragover=\"return false\" ondrop=\"drop(this, event)\"\>

41.      \<p\>Drop some text selection here.\</p\>

42. \</div\>

43. \</body\>

44. \</html\>

Here, we use a CSS trick to make the second paragraph non-selectable, by
setting the user-selected property to none.

In the next chapter, we will see how to drag and drop files!

## 3.3.9 Discussion and projects

Here is the discussion forum for this part of the course. Please either
post your comments/observations/questions or share your creations.

### Suggested topics of discussion:

-   If you find interesting drag and drop examples on the Web, please
    share them in the forum.

-   What other example(s) would you like to be added to the course (drag
    and drop of files is covered in the next lesson)?

### Optional projects:

-   Code an illustrative drag and drop demo, and share it in the forum.
    For example, try to add something similar to the \"what is your
    preferred fruit\" or \"what is your preferred browser\" to a form.

-   Order a set of images by dragging and dropping them. A sort of
    picture gallery, you drag one picture (an \<img\> element) from its
    current position and drop it at another location in the gallery (a
    grid). In the meantime, the other pictures will have to move to give
    some room for the picture you dropped.

## 3.4.1 Introduction

In these lectures, we will learn how to *drag and drop files* between
the browser and the desktop. The process shares similarities with the
methods for *dragging and dropping elements* within an HTML document,
but it\'s even simpler!

### Drag and drop files from the desktop to the browser: the files property of the clipboard

The principle is the same as in the examples from the previous section
(drag and drop basics), except that we do not need to worry about
a dragstart handler. **Files will be dragged from the desktop, so the
browser only has to copy their content from the clipboard** and make it
available in our JavaScript code.

Indeed, **the main work will be done in the drop handler**, where we
will use the *files property* of the *dataTransfer object* (aka the
clipboard). This is where the browser will copy the files that have been
dragged from the desktop. 

This *files object* is the same one we saw in the chapter about the File
API in the \"HTML5 part 1\" course: it is a collection
of *file objects* \>(sort of file descriptors). From each file object,
we will be able to extract the name of the file, its type, size, last
modification date, read it, etc.

In this source code extract we have a *drop* handler that works on files
which have been dragged and dropped from the desktop to a drop zone
associated with this handler with
an ondrop=dropHandler(event); attribute:

1.  function dropHandler(event) {

2.     // Do not propagate the event

3.     event.stopPropagation();

4.     // Prevent default behavior, in particular when we drop images or
    links

5.     event.preventDefault();

6.  

7.     **// get the dropped files from the clipboard**

8.     **var files = event.dataTransfer.files;**

9.  

10.    var filenames = \"\";

11. 

12.    // do something with the files\...here we iterate on them and log
    the filenames

13.    for(var i = 0 ; i \< files.length ; i++) {

14.        filenames += \'\\n\' + files\[i\].name;

15.    }

16. 

17.    console.log(files.length + \' file(s) have been
    dropped:\\n\' + filenames);

18. }

At *lines 7-8*, we get the files that have been dropped.

*Lines 12-15* iterate over the collection and build a string which
contains the list of file names.

*Line 17* displays this string on the debugging console.

Complete working examples are to be presented later on\...

### Prevent the browser\'s default behavior

If we drop an image into an HTML page, the browser will open a new tab
and display the image. With a .mp3 file, it will open it in a new tab
and a default player will start streaming it, etc. We need to prevent
this behavior in order to customisethe processing of the dropped files
(i.e. display an image thumbnail, add entries to a music playlist,
etc.). So, when dragging and dropping images or links, we need to
prevent the browser\'s default behavior.

At the beginning of the drop handler in the previous piece of code, you
can see the lines of code (*lines 2-5*) that stop the propagation of the
drop event and prevent the default behavior of the browser. Normally
when we drop an image or an HTTP link onto a web page, the browser will
display the image or the web page pointed by the link, in a new
tab/window. This is not what we would like in an application using the
drag and drop process. These two lines are necessary to prevent the
default behavior of the browser:

1.  // Do not propagate the event

2.  event.stopPropagation();

3.  // Prevent default behavior, in particular when we drop images or
    links

4.  event.preventDefault();

> **Best practice**: add these lines tothe drop handler AND
> to the dragOver handler attached to the drop zone!

\... like in this example:

1.  function dragOverHandler(event) {

2.     // Do not propagate the event

3.     event.stopPropagation();

4.  

5.     // Prevent default behavior, in particular when we drop images or
    links

6.     event.preventDefault();

7.     \...

8.  }

9.  

10. function dropHandler(event) {

11.    // Do not propagate the event

12.    event.stopPropagation();

13. 

14.    // Prevent default behavior, in particular when we drop images or
    links

15.    event.preventDefault();

16.    \...

17. }

### External resources

-   Web.dev article: \"[Using the HTML5 drag and drop
    API](https://web.dev/drag-and-drop/)\"

-   HTML Goodies article: \"[Drag Files Into the Browser From the
    Desktop with
    HTML5](https://www.htmlgoodies.com/html5/javascript/drag-files-into-the-browser-from-the-desktop-HTML5.html)\"

## 3.4.2 Drag and drop files in a drop zone

Hi! This time let\'s look at how we can drag and

drop files into a document. So, the first thing you must know is that,

by default, the browser does things when you drag and drop.

If I drag and drop an image, it just shows the image in full size in a
new tab.

If I drag and drop a video, the browser will just play it using a
default player.

So, if you want to drag and drop some multimedia files, we will have to
take care and prevent

this default behavior. So first, let\'s look at a more simple example.

We will just drag and drop files, one or multiple files into a drop
zone.

The first thing you must know... (ok, I wanted to drag and drop multiple
files but I missed

the multiple selection...) OK, it work with multiple files.

So the first thing you must know is that we can\'t have a dragstart
handler, there is no

need for a dragstart handler. As soon as you drop files in a document,
the file descriptors

are copied in the drag and drop clipboard. The source code is much
simpler than the one

we saw in the previous videos. So here we define a drop zone, a div
called

droppableZone, with a dragenter, drop, dragover and dragleave event
listeners. We also created

an empty numbered list inside the div ... this is the container that
will be used to display the

file names here. What do we do in order to prevent this default
behavior?

Because if I drag and drop an image in this

div without taking some precautions, it will just open a new tab with
the image.

So, in the different drop and dragover handlers we will have to call
event.preventDefault()

for preventing this default behavior and we also call stopPropagation(),
so that the event

will not go to the parents of the div\... and in case they will also
have this default behavior

triggered. As we don\'t have any dragstart handler, and

the files are copied directly into the drag and drop clipboard, we get
back the files

using event.dataTransfer.files. We are not using a key to get the value
here,

it is just files. It is the same name and the same content we got when
we use an onchange

listener on an input type=\"file\". Each element (from files) has the
same properties

we saw in the HTML5 Part 1 course about forms, and in particular about
the input type=\"file\".

We get the files that have been copied into the clipboard and then we do
a loop on the

files, we get the current file name here, and we create a list item and
we just set

the text content. Then we append the list item that has the file name as
its content,

to the dropped zone. That\'s all, it is very easy, you drag and

drop files\... in the drop handler you stop the propagation, prevent the
default behavior,

get the files property with all the files copied, do a loop and process
them. That\'s all. Bye, bye!

### Example: drag and drop files to a drop zone, display file details in a list

![Example of drag\'n\'drop of a
file](./images/image018.jpeg){width="4.645833333333333in"
height="3.8958333333333335in"}

Try the example below directly in your browser (just drag and drop
files to the greyish drop zone), or [play with it at
CodePen](https://codepen.io/w3devcampus/pen/JYjpqV?editors=111):

Complete source code from the example:

1.  \<!DOCTYPE html\>

2.  \<html lang=\"en\"\>

3.  \<head\>

4.     \<style\>

5.        div {

6.           height: 150px;

7.           width: 350px;

8.           float: left;

9.           border: 2px solid #666666;

10.          background-color: #ccc;

11.          margin-right: 5px;

12.          border-radius: 10px;

13.          box-shadow: inset 0 0 3px #000;

14.          text-align: center;

15.          cursor: move;

16.       }

17. 

18.       .dragged {

19.          border: 2px dashed #000;

20.          background-color: green;

21.       }

22. 

23.       .draggedOver {

24.          border: 2px dashed #000;

25.          background-color: green;

26.       }

27.  

28.     \</style\>

29.     \<script\>

30.       function dragLeaveHandler(event) {

31.           console.log(\"drag leave\");

32.           // Set style of drop zone to default

33.           event.target.classList.remove(\'draggedOver\');

34.       }

35. 

36.       function dragEnterHandler(event) {

37.           console.log(\"Drag enter\");

38.           // Show some visual feedback

39.           event.target.classList.add(\'draggedOver\');

40.       }

41. 

42.       function dragOverHandler(event) {

43.           //console.log(\"Drag over a droppable zone\");

44.           // Do not propagate the event

45.           event.stopPropagation();

46.           // Prevent default behavior, in particular when we drop
    images or links

47.           event.preventDefault();

48.       }

49. 

50.       function dropHandler(event) {

51.           console.log(\'drop event\');

52. 

53.           // Do not propagate the event

54.           event.stopPropagation();

55.           // Prevent default behavior, in particular when we drop
    images or links

56.           event.preventDefault();

57. 

58. 

59.           // reset the visual look of the drop zone to default

60.           event.target.classList.remove(\'draggedOver\');

61. 

62. 

63.           // get the files from the clipboard

64.           var files = event.dataTransfer.files;

65.           var filesLen = files.length;

66.           var filenames = \"\";

67. 

68.           // iterate on the files, get details using the file API

69.           // Display file names in a list.

70.           for(var i = 0 ; i \< filesLen ; i++) {

71.               filenames += \'\\n\' + files\[i\].name;

72.               // Create a li, set its value to a file name, add it
    to the ol

73.               var li = document.createElement(\'li\');

74.              
    li.textContent = files\[i\].name; document.querySelector(\"#droppedFiles\").appendChild(li);

75.           }

76.           console.log(files.length + \' file(s) have been
    dropped:\\n\' + filenames);

77.       }

78.   \</script\>

79. \</head\>

80. \<body\>

81.   \<h2\>Drop your files here!\</h2\>

82.   \<div id=\"droppableZone\" ondragenter=\"dragEnterHandler(event)\" ondrop=\"dropHandler(event)\" 
       

83.                           ondragover=\"dragOverHandler(event)\" 
     ondragleave=\"dragLeaveHandler(event)\"\>

84.      Drop zone

85.      \<ol id=\"droppedFiles\"\>\</ol\>

86.   \</div\>

87. \<body\>

88. \<html\>

Note that:

-   We prevented the browser default behavior in
    the drop and dragover handlers Otherwise, if we dropped a media file
    (an image, an audio of video file), the browser would try to
    display/play it in a new window/tab. We also stop the  propagation
    for performance reasons, because when we drag an object it can
    raise many events within the parents of the drop zone element as
    well.

-   *Lines 73-74* create a \<li\> element. Its value is initialized with
    the file name of the current file in the collection, and added to
    the \<ol\> list.

In principle, this example is very similar to the \"fruit\" examples we
worked through earlier, except that this time we\'re working with
files. *And when we work with files, it is important to prevent the
browser\'s default behavior.*

## 3.4.3 Images with thumbnails

This time, let\'s reuse the readFilesAndDisplayPreview() method (studied
in the W3Cx HTML5 Coding Essentials and Best Practices course). We have
reproduced the example here - please review the source code to refresh
your memory (click on the JS tab or [look at the example at
CodePen](https://codepen.io/w3devcampus/pen/ZbExbM)).

Click the \"Choose files\" button (an \<input type=\"file\"\> element),
select one or more images \-- and you should see image thumbnails
displayed in the open space beneath it:

![](./images/image019.png){width="6.5in"
height="1.832638888888889in"}

Source code extract (the part that reads the image file content and
displays the thumbnails):

1.  function readFilesAndDisplayPreview(files) {

2.     // Loop through the FileList and render image files

3.     // as thumbnails.

4.     for (var i = 0, f; f = files\[i\]; i++) {

5.  

6.       // Only process image files.

7.       if (!f.type.match(\'image.\*\')) {

8.          continue;

9.       }

10. 

11.      var reader = new FileReader();

12. 

13.      //capture the file information.

14.      reader.onload = function(e) {

15.          // Render thumbnail.

16.          var span = document.createElement(\'span\');

17.          span.innerHTML = \"\<img class=\'thumb\' src=\'\" +

18.                            e.target.result + \"\'/\>\";

19.          document.getElementById(\'list\').insertBefore(span, null);

20.      };

21. 

22.      // Read the image file as a data URL. Will trigger

23.      // a call to the onload callback above

24.      // only once the image is completely loaded

25.      reader.readAsDataURL(f);

26.    }

27. }

At *line7*, there is a test that will avoid processing non image files.
The \"!\" is the NOT operator in JavaScript. The call to continue
at *line 8* will make the for loop go to its end and process the next
file. See the HTML5 part 1 course about the file API for more details
(each file has a name, type, lastModificationDate and size attribute.
The call to match(\...) here is a standard way in JavaScript to match a
string value with a regular expression).

At *line 19*, we insert the \<img\> element that was created and
initialized with the dataURL of the image file, into the HTML list with
an id of \"list\".

So, let\'s add this method to our code example, to display file details
once dropped, and also add an \<output id=\"list\"\>\</output\> to the
HTML of this example.

#### Complete example of drag and drop + thumbnails of images

![ilmage drag\'n\'drop with
thumbnails](./images/image020.jpeg){width="6.5in"
height="4.05625in"}

Try it below in your browser (drag\'n\'drop image files into the drop
zone) or play with it at CodePen:

Complete source code:

1.  \<!DOCTYPE html\>

2.  \<html lang=\"en\"\>

3.  \<head\>

4.      \<style\>

5.         div {

6.            height: 150px;

7.            width: 350px;

8.            border: 2px solid #666666;

9.            background-color: #ccc;

10.           margin-right: 5px;

11.           border-radius: 10px;

12.           box-shadow: inset 0 0 3px #000;

13.           text-align: center;

14.           cursor: move;

15.        }

16. 

17.        .dragged {

18.           border: 2px dashed #000;

19.           background-color: green;

20.        }

21. 

22.        .draggedOver {

23.           border: 2px dashed #000;

24.           background-color: green;

25.        }

26. 

27.      \</style\>

28.      \<script\>

29.        function dragLeaveHandler(event) {

30.           console.log(\"drag leave\");

31.           // Set style of drop zone to default

32.           event.target.classList.remove(\'draggedOver\');

33.        }

34. 

35.        function dragEnterHandler(event) {

36.           console.log(\"Drag enter\");

37.           // Show some visual feedback

38.           event.target.classList.add(\'draggedOver\');

39.        }

40. 

41.        function dragOverHandler(event) {

42.           //console.log(\"Drag over a droppable zone\");

43.           // Do not propagate the event

44.           event.stopPropagation();

45.           // Prevent default behavior, in particular when we drop
    images or links

46.           event.preventDefault();

47.        }

48. 

49.        function dropHandler(event) {

50.           console.log(\'drop event\');

51. 

52.           // Do not propagate the event

53.           event.stopPropagation();

54.           // Prevent default behavior, in particular when we drop
    images or links

55.           event.preventDefault();

56. 

57.           // reset the visual look of the drop zone to default

58.           event.target.classList.remove(\'draggedOver\');

59. 

60. 

61.           // get the files from the clipboard

62.           var files = event.dataTransfer.files;

63.           var filesLen = files.length;

64.           var filenames = \"\";

65. 

66.           // iterate on the files, get details using the file API

67.           // Display file names in a list.

68.           for(var i = 0 ; i \< filesLen ; i++) {

69.              filenames += \'\\n\' + files\[i\].name;

70.              // Create a li, set its value to a file name, add it to
    the ol

71.              var li = document.createElement(\'li\');

72.              li.textContent = files\[i\].name;

73.            
     document.querySelector(\"#droppedFiles\").appendChild(li);

74.           }

75.           console.log(files.length + \' file(s) have been
    dropped:\\n\' + filenames);

76. 

77.           readFilesAndDisplayPreview(files);

78.        }

79. 

80.        function readFilesAndDisplayPreview(files) {

81.           // Loop through the FileList and render image files as
    thumbnails.

82.           for (var i = 0, f; f = files\[i\]; i++) {

83. 

84.           // Only process image files.

85.           if (!f.type.match(\'image.\*\')) {

86.              continue;

87.           }

88. 

89.           var reader = new FileReader();

90. 

91.           //capture the file information.

92.           reader.onload = function(e) {

93.              // Render thumbnail.

94.              var span = document.createElement(\'span\');

95.              span.innerHTML = \"\<img class=\'thumb\' width=\'100\'
    src=\'\" + e.target.result + \"\'/\>\";

96.            
     document.getElementById(\'list\').insertBefore(span, null);

97.           };

98. 

99.           // Read the image file as a data URL. Will trigger the
    call to the above callback when

100.           // the image file is completely loaded

101.           reader.readAsDataURL(f);

102.        }

103.     }

104.   \</script\>

105. \</head\>

106. \<body\>

107. \<h2\>Drop your files here!\</h2\>

108. \<div id=\"droppableZone\" ondragenter=\"dragEnterHandler(event)\" ondrop=\"dropHandler(event)\"

109.                          ondragover=\"dragOverHandler(event)\" 
      ondragleave=\"dragLeaveHandler(event)\"\>

110.     Drop zone

111.     \<ol id=\"droppedFiles\"\>\</ol\>

112. \</div\>

113. \<br/\>

114. \<output id=\"list\"\>\</output\>

115. \<body\>

116. \<html\>

Above, we added the readFilesAndDisplayPreview() method detailed
earlier. We called it at the end of the drop handler (*line 77*), and we
added the \<output\> element as a container for the \<img\> elements
(constructed by the JavaScript code *lines 94-96*) which will display
the thumbnails (*line 114*).

## 3.4.4 Mixing drag and drop and input type=file

Let\'s go further and also add an \<input type=\"file\"\>

The example below allows files to be selected using a file chooser or by
drag  and dropping them, like in the screenshot below (the interactive
example is a bit further down the page):

![example of file chooser and dir
chooser](./images/image021.png){width="6.5in"
height="6.3694444444444445in"}

In the above screenshot, which is derived from the example detailed
later in this page, we selected some files using the first button (which
is an \<input type=\"file\" multiple\.../\>),then we used the second
button (which is an \<input type=\"file\" webkitdirectory\>) to select a
directory that contained 11 files. We then dragged and dropped some
other images to the drop zone. Each time, thumbnails were displayed.
Both methods (file selector or drag and drop) produced the same result.

#### Idea: reuse the same code for reading image files and displaying thumbnails

If you look (again) at [the very first example that displayed
thumbnails, without drag and
drop)](https://codepen.io/w3devcampus/pen/ZbExbM), you will notice that
the event handler we used to track the selected files using \<input
type=\"file\"/\> looks like this:

1.  \<script\>

2.     function handleFileSelect(evt) {

3.         var files = evt.target.files; // FileList object

4.         // do something with files\... why not call
    readFilesAndDisplayPreview!

5.         **readFilesAndDisplayPreview(files);**

6.     }

7.  

8.   
     document.getElementById(\'files\').addEventListener(\'change\', handleFileSelect, false);

9.  \</script\>

10. \...

11. \<body\>

12.    Choose multiple files
    :\<input type=\"file\" id=\"files\" multiple /\>\<br/\>

13. \</body\>

It calls readFilesAndDisplayPreview()at *line 5*! The same function with
the same parameters is also used by [the example that used drag and drop
that we discussed on a previous page of this
course.](https://codepen.io/w3devcampus/pen/XmWEMQ) 

Let\'s mix both examples: add to our drag\'n\'drop example an \<input
type=\"file\"\> element, and the above handler. This will allow us to
select files either with drag\'n\'drop or by using a file selector.

Just for fun, we also added [an experimental \"directory chooser\" that
is thus far only implemented by Google
Chrome](https://www.youtube.com/watch?v=WaSP-rdQA_c) (notice, \<input
type=\"file\" webkitdirectory\> is **not** in the HTML5 specification.
Drag and drop functionality will work through a file chooser in any
modern browser, but the directory chooser will only work with Google
Chrome).

### Complete interactive example with source code

Try it in your browser below (use all three functions: firstly using
the file selector, secondly the directory selector, and finally to drag
and drop image files into the drop zone), or [play with it at
CodePen](https://codepen.io/w3devcampus/pen/BoavPb):

Complete source code:

1.  \<!DOCTYPE html\>

2.  \<html lang=\"en\"\>

3.  \<head\>

4.     \<style\>

5.        div {

6.            height: 150px;

7.            width: 350px;

8.            border: 2px solid #666666;

9.            background-color: #ccc;

10.           margin-right: 5px;

11.           border-radius: 10px;

12.           box-shadow: inset 0 0 3px #000;

13.           text-align: center;

14.           cursor: move;

15.       }

16.  

17.       .dragged {

18.           border: 2px dashed #000;

19.           background-color: green;

20.       }

21. 

22.       .draggedOver {

23.           border: 2px dashed #000;

24.           background-color: green;

25.       }

26.  

27. \</style\>

28. \<script\>

29.       function dragLeaveHandler(event) {

30.          console.log(\"drag leave\");

31.          // Set style of drop zone to default

32.          event.target.classList.remove(\'draggedOver\');

33.       }

34. 

35.       function dragEnterHandler(event) {

36.          console.log(\"Drag enter\");

37.          // Show some visual feedback

38.          event.target.classList.add(\'draggedOver\');

39.       }

40. 

41.       function dragOverHandler(event) {

42.          //console.log(\"Drag over a droppable zone\");

43.          // Do not propagate the event

44.          event.stopPropagation();

45.          // Prevent default behavior, in particular when we drop

46.          // images or links

47.          event.preventDefault();

48.       }

49. 

50.       function dropHandler(event) {

51.          console.log(\'drop event\');

52. 

53.          // Do not propagate the event

54.          event.stopPropagation();

55.          // Prevent default behavior, in particular when we drop

56.          // images or links

57.          event.preventDefault();

58. 

59. 

60.          // reset the visual look of the drop zone to default

61.          event.target.classList.remove(\'draggedOver\');

62. 

63. 

64.          // get the files from the clipboard

65.          var files = event.dataTransfer.files;

66.          var filesLen = files.length;

67.          var filenames = \"\";

68. 

69.          // iterate on the files, get details using the file API

70.          // Display file names in a list.

71.          for(var i = 0 ; i \< filesLen ; i++) {

72.             filenames += \'\\n\' + files\[i\].name;

73.             // Create a li, set its value to a file name, add it to
    the ol

74.             var li = document.createElement(\'li\');

75.             li.textContent = files\[i\].name;

76.            
    document.querySelector(\"#droppedFiles\").appendChild(li);

77.          }

78.          console.log(files.length + \' file(s) have been
    dropped:\\n\' + filenames);

79. 

80.          **readFilesAndDisplayPreview(files);**

81.       }

82. 

83.       function readFilesAndDisplayPreview(files) {

84.          // Loop through the FileList and render image files as

85.          // thumbnails.

86.          for (var i = 0, f; f = files\[i\]; i++) {

87. 

88.             // Only process image files.

89.             if (!f.type.match(\'image.\*\')) {

90.                continue;

91.             }

92. 

93.             var reader = new FileReader();

94. 

95.             //capture the file information.

96.             reader.onload = function(e) {

97.                // Render thumbnail.

98.                var span = document.createElement(\'span\');

99.                span.innerHTML = \"\<img class=\'thumb\'
    width=\'100\' src=\'\" +

100.                                 e.target.result + \"\'/\>\";

101.              
      document.getElementById(\'list\').insertBefore(span, null);

102.             };            

103.            // Read the image file as a data URL.

104.            reader.readAsDataURL(f);

105.         }

106.      }

107. 

108.      **function handleFileSelect(evt) {**

109.         **var files = evt.target.files; // FileList object**

110.         **// do something with files\... why not call**

111. **        // readFilesAndDisplayPreview!**

112.        **readFilesAndDisplayPreview(files);**

113.      }

114.   \</script\>

115. \</head\>

116. \<body\>

117. \<h2\>Use one of these input fields for selecting files\</h2\>

118. \<p\>Beware, the directory choser  may overload

119. your browser memory if there are too many big images in the

120. directory you choose.\</p\>

121. **Choose multiple files
     :** **\<input type=\"file\" id=\"files\" multiple**

122. **                             
      onchange=\"handleFileSelect(event)\"/\>**

123. \</p\>

124. **\<p\>Choose a directory (Chrome only): \<input type=\"file\"**

125. **                                     
     id=\"dir\" webkitdirectory**

126. **                                     
     onchange=\"handleFileSelect(event)\"/\>**

127. \</p\>

128.  

129. \<h2\>Drop your files here!\</h2\>

130.  
       \<div id=\"droppableZone\" ondragenter=\"dragEnterHandler(event)\"

131.                             ondrop=\"dropHandler(event)\"

132.                             ondragover=\"dragOverHandler(event)\"

133.                            
     ondragleave=\"dragLeaveHandler(event)\"\>

134.         Drop zone

135.         \<ol id=\"droppedFiles\"\>\</ol\>

136.      \</div\>

137. \<br/\>

138. \<output id=\"list\"\>\</output\>

139. \<body\>

140. \<html\>

The parts that we have added are in bold. As you can see, all methods
share the same code for previewing the images.

## 3.4.5 Files upload using Ajax/XHR2

This time, let us mash-up a couple of examples. Let\'s combine the
upload of files using XHR2, with progress monitoring (we worked on in
the 3.2 lectures) with one of our drag and drop examples. To achieve
this, we re-use the method calleduploadAllFilesUsingAjax() and add
a \<progress\> element to the drag and drop example.

[Try this interactive example at
JSBin](https://jsbin.com/conigekoda/edit) (this example does not work on
CodePen. We are using a fake remote server and it cancels the connection
as soon as we try to connect):

![example that uses drag\'n\'drop and a progress element for monitoring
the ajax upload of the
files](./images/image022.jpeg){width="4.364583333333333in"
height="2.90625in"}

Source code extract (we omitted the CSS):

1.  \<!DOCTYPE html\>

2.  \<html\>

3.  \<head\>

4.     \<style\>

5.       \...

6.     \</style\>

7.     \<script\>

8.       function dragLeaveHandler(event) {

9.         console.log(\"drag leave\");

10.        // Set style of drop zone to default

11.        event.target.classList.remove(\'draggedOver\');

12.      }

13. 

14.      function dragEnterHandler(event) {

15.        console.log(\"Drag enter\");

16.        // Show some visual feedback

17.        event.target.classList.add(\'draggedOver\');

18.      }

19. 

20.      function dragOverHandler(event) {

21.        //console.log(\"Drag over a droppable zone\");

22.        // Do not propagate the event

23.        event.stopPropagation();

24.        // Prevent default behavior, in particular when we drop
    images

25.        // or links

26.        event.preventDefault();

27.      }

28. 

29.      function dropHandler(event) {

30.        console.log(\'drop event\');

31. 

32.        // Do not propagate the event

33.        event.stopPropagation();

34.        // Prevent default behavior, in particular when we drop
    images

35.        // or links

36.        event.preventDefault();

37. 

38.        // reset the visual look of the drop zone to default

39.        event.target.classList.remove(\'draggedOver\');

40. 

41. 

42.        // get the files from the clipboard

43.        var files = event.dataTransfer.files;

44.        var filesLen = files.length;

45.        var filenames = \"\";

46. 

47.        // iterate on the files, get details using the file API

48.        // Display file names in a list.

49.        for(var i = 0 ; i \< filesLen ; i++) {

50.           filenames += \'\\n\' + files\[i\].name;

51.           // Create a li, set its value to a file name, add it to
    the ol

52.           var li = document.createElement(\'li\');

53.           li.textContent = files\[i\].name;

54.           document.querySelector(\"#droppedFiles\").appendChild(li);

55.        }

56.        console.log(files.length + \' file(s) have been dropped:\\n\'

57.                                 + filenames);

58. 

59.        uploadAllFilesUsingAjax(files);

60.      }

61. 

62.      function uploadAllFilesUsingAjax(files) {

63.        var xhr = new XMLHttpRequest();

64.        xhr.open(\'POST\', \'upload.html\');

65. 

66.        xhr.upload.onprogress = function(e) {

67.           progress.value = e.loaded;

68.           progress.max = e.total;

69.        };

70. 

71.        xhr.onload = function() {

72.          alert(\'Upload complete!\');

73.        };

74. 

75.        var form = new FormData();

76.        for(var i = 0 ; i \< files.length ; i++) {

77.           form.append(\'file\', files\[i\]);

78.        }

79.  

80.        // Send the Ajax request

81.        xhr.send(form);

82.      }

83.   \</script\>

84. \</head\>

85. \<body\>

86. \<h2\>Drop your files here!\</h2\>

87. \<div id=\"droppableZone\" ondragenter=\"dragEnterHandler(event)\"

88.                          ondrop=\"dropHandler(event)\"

89.                          ondragover=\"dragOverHandler(event)\"     

90.                          ondragleave=\"dragLeaveHandler(event)\"\>

91.      Drop zone

92.      \<ol id=\"droppedFiles\"\>\</ol\>

93. \</div\>

94. \<br/\>

95.  Uploading progress: \<progress id=\"progress\"\>\</progress\>

96. \<body\>

97. \<html\>

We have highlighted the interesting parts in the example!

We build *(line 75)* an object of type FormData (this comes from the
standard JavaScript DOM API level 2), we fill this object with the file
contents (*line 77*), then we send the Ajax request (*line 81*), and
monitor the upload progress (*lines 66-69*).

Instead of uploading all the files at once, it might be interesting to
upload one file at a time with visual feedback, such as: \"uploading
file MichaelJackson.jpg\.....\". We will leave this exercise up to you.

## 3.4.6 Discussion and projects

Here is the discussion forum for this part of the course. Please either
post your comments/observations/questions or share your creations.

### Suggested topics of discussion:

-   Did you know that it was possible to gain control over the process
    of dragging a file out of a page, and dropping it onto the desktop
    (for example)?

### Optional projects:

-   If a user were to drag and drop the same file to a drop zone several
    times, this would be confusing. Try to modify some of the examples
    to avoid duplication (i.e.: not uploading the same file twice).

-   Try to modify the example that played a song loaded in memory, using
    Web Audio, for allowing a song file to be dragged and dropped.

-   Combine these topics with the talents you developed earlier, working
    with canvas: instead of a progress \'thermometer\' to measure XHR2
    upload progress, try modifying the appearance of the thumbnail to
    show the proportion of the graphic file as it is transferred
    (alternatively, if you have style-sheet skills, you could try this
    using CSS transitions).

## 3.5.1 Introduction

We had many questions about how to submit a form with regular input
fields AND benefit from the HTML5 built-in validation AND upload files
AND monitor the file upload progress with a progress bar.

Many solutions proposed on the Web rely on jQuery plugins. However,
coding such a behavior using only HTML5 APIs is easy AND faster AND has
a lower *page weight*, as we will see.

This part of the course will describe different approaches for
implementing file uploads associated with a form.

We have included PHP server-side code: this course focuses on HTML5 and
front-end development - so, the PHP code is given \"as is\".

### The problem

Imagine that we have a regular HTML5 form, but as well as the input
fields for entering a name, address, age, etc., we also want to select
and upload multiple files (which might include images). 

### Serial approach: upload the files as soon as they are selected or dragged and dropped

Let\'s design an XHR2/Ajax, a form with an \<input type=file
multiple\> input field, and one or more \<progress\> elements for
monitoring file uploads. The form will also have input fields of
different types.

An example of this kind of form is shown below: when the user drags and
drops files, they will start being uploaded immediately. However,  the
form will only be sent when all the fields are valid. 

![uploading files using Xhr2, drag\'n\'drop and progress
bar](./images/image023.jpeg){width="6.5in"
height="3.982638888888889in"}

This approach is similar to Gmail\'s behavior when you compose a message
and add an attachment. The attachments are uploaded as soon as they are
selected or dropped into the message window, but the message will only
be sent when you press the \"send\" button. An empty field with
a required attribute, if left empty, will cause an error message pop
up in a bubble, and the form will not be submitted. Nice!

However, on the server side, we need a way to \"join\" the files that
have been asynchronously uploaded with the rest of the form\'s
values. This is easier to do than it sounds. Look at the provided PHP
code provided with each of the examples.

### Packaged approach: send all form content, including files, only when the form is submitted

-   This method enables us to send all of the form\'s content (regular
    input field values + files selected) at once, *using a single Ajax
    request* (we will need only one progress bar),

-   or we may *use multiple Ajax requests*, which we don\'t start until
    the submit button has been clicked.

![Second approach, send files only when the sublit button has been
clicked](./images/image024.jpeg){width="6.291666666666667in"
height="2.3229166666666665in"}

The difference between this and the first approach is that we are
sending everything *at the same time* using Ajax/JavaScript: the regular
input field content and the selected files.

The next page provides the source code of several examples, as well as
the server-side PHP code.

## 3.5.2 Installation guide

Please download all examples (authors: Michel Buffa, improvements and
fixes by Vincent Mazenod): [Zip file containing all examples (html +
css + js + php +
readmes)](https://courses.edx.org/assets/courseware/v1/5909531330a0343fa4499895a2de137d/asset-v1:W3Cx+HTML5.2x+2T2020a+type@asset+block/forms_php_upload.zip)

The examples can be tried online at JSBin (see in the following pagesà,
but the upload is \"faked\". These online examples do not use a real
server, but are useful for playing with the code and understanding how
it works. You can try them and see uploads\' progress, etc.

However, we also provide complete source code for these examples,
including the server-side PHP code. The course is about HTML5, not PHP,
so we provide this code \"as is\": it is only a few lines long per
example, and has been tested with the latest version of PHP.  It should
run out of the box with most WAMP, LAMP, and MAMP distributions (Apache
/ PHP).

Unzip the archive and follow the included READMEs. These examples
propose **different implementations of the two approaches** presented in
the previous lecture, and both with an \<input type=file\> and drag and
drop.

The HTML part of the examples is also using a technique, seen during the
W3Cx HTML5 Coding Essentials course, that saves the input fields\'
content as you type, using LocalStorage. You can reload the page any
time without losing what you typed. Initially, the examples all used a
FormData object but at the time we encountered some incompatibilities
with older versions of PHP, so we had to manually set a component of the
HTTP header.

This part of the lesson is optional and is mainly useful for students
who are also involved in the server side of the Web development.

## 3.5.3 Serial approach

We made two examples that rely on the serial approach:

1.  one that uses only a file selector,

2.  one that uses drag and drop.

We could have merged file selector + drag and drop, as we did in
examples earlier in the course, but the code would have been longer and
more difficult to follow.

### Example #1: auto-loading of the files, regular form submission, benefits of the HTML5 form validation system

Example using a file selector (\<input type=\"file\"\>):

![example 1 of file
upload](./images/image025.png){width="4.854166666666667in"
height="1.7916666666666667in"}

[Try the online example at
JSBin](https://jsbin.com/rozanow/edit?html,css,js,output) (this one does
not have the PHP code running, but works anyway, even if the files are
not uploaded - it \"fakes the upload\"). Look at the online example for
the code and the following explanations.

In this example, the \"send\" button is disabled and becomes enabled as
soon as all the files are completely uploaded. Also, note that the form
is saved as the user types, by using localStorage. Accordingly, it can
be restored on page reload, as in the example from the localStorage
topic of the HTML5 Part 1 course.

Note that the full working source code of this example corresponds to
\"example 1\" [in the zip archive that contains all
examples](https://courses.edx.org/assets/courseware/v1/e694f9e43a0ef0139fb57f71fae0d0ed/asset-v1:W3Cx+HTML5.2x+2T2020a+type@asset+block/upload.zip).

### Example #2: similar example but using drag and drop instead of a file selector

Here is much the same code, but this time it uses drag and drop to
collect the filenames, not an input field. [Try it at
JSBin](https://jsbin.com/qijoza/edit?html,css,js,output) and look at the
source code - there are plenty of comments.

![example 2 of file uploads, uses
drag\'n\'drop](./images/image026.png){width="6.5in"
height="3.982638888888889in"}

### And here is the PHP code for the server-side part of examples #1 and #2

This code is given \"as is\":

1.  \<?php

2.  

3.  if (isset(\$\_POST\[\'givenname\'\]) && isset(\$\_POST\[\'familyname\'\])) {

4.     echo \$\_POST\[\'givenname\'\].\'
    \'.\$\_POST\[\'familyname\'\].\' uploaded file(s).\<br /\>\';

5.  }

6.  

7.  if (isset(\$\_POST\[\'namesAllFiles\'\]) && \$\_POST\[\'namesAllFiles\'\] != \"\") {

8.    \$folderName = date(\"m.d.Y\");

9.    if (!is_dir(\'upload/\'.\$folderName)) {

10.      mkdir(\'upload/\'.\$folderName);

11. }

12. 

13. \$filesName = explode(\"::\", \$\_POST\[\'namesAllFiles\'\]);

14.   for (\$i=0; \$i \< count(\$filesName); \$i++) {

15.     copy(\'upload/RecycleBin/\'.\$filesName\[\$i\],

16.          \'upload/\'.\$folderName.\'/\'.\$filesName\[\$i\]);

17.     unlink(\'upload/RecycleBin/\'.\$filesName\[\$i\]);

18.     echo \"\$filesName\[\$i\] uploaded\<br /\>\";

19.   }

20. }

21. 

22. \$fn = (isset(\$\_SERVER\[\'HTTP_X_FILENAME\'\]) ?

23.                                
     \$\_SERVER\[\'HTTP_X_FILENAME\'\] : false);

24. 

25. if (\$fn) {

26.   if (!is_dir(\'upload/RecycleBin\')) {

27.     mkdir(\'upload/RecycleBin\');

28.   }

29.   file_put_contents(\'upload/RecycleBin/\'.\$fn,     

30.                     file_get_contents(\'php://input\'));

31.   exit();

32. }

33. 

34. ?\>

**Explanations**:

-   When files are first uploaded, they are stored in a directory
    called upload/RecycleBin. If it does not exist, this directory is
    created (*lines 22-32*).

-   When the form is submitted, a directory whose name is today\'s date
    is created, and the files located in the RecycleBin directory are
    moved to that directory. If it does not already exist, the directory
    will be created  (*lines 7-20*).

## 3.5.4 Package approach

Let\'s use the previous two examples as a basis for two further
examples:

1.  one that uses only a file selector,

2.  one that uses drag and drop.

### Example #3: uploading everything at once using a file selector

A file selector (\<input type=\"file\"\>).

This time, we add the files to an HTML5 FormData object before sending
XHR2 Ajax requests to the server (one for each file + one for the rest
of the form).  The uploads only start once the form is submitted.

You can [try this example at
JSBin](https://jsbin.com/quzohi/edit?html,css,js,output), and look at
the source code and comments for details.

![Example 3 of file
uploads](./images/image027.png){width="6.072916666666667in"
height="2.1770833333333335in"}

### Example #4: uploading using drag and drop

[Try the example at
JSBin](https://jsbin.com/xonemow/edit?html,css,output) and look at
source code and comments.

![Example 4: uses drag\'n\'drop of
files](./images/image028.png){width="5.385416666666667in"
height="3.71875in"}

### PHP code for the single-packaged examples (with and without drag and drop, the PHP is the same)

This code is given \"as is\". The principle is the same as with the
examples given in the previous section, except that this time we do not
have to deal with a temporary \"RecycleBin\" directory.

1.  \<?php

2.  

3.  if (isset(\$\_POST\[\'givenname\'\]) && isset(\$\_POST\[\'familyname\'\])) {

4.      echo \$\_POST\[\'givenname\'\] . \'
    \' . \$\_POST\[\'familyname\'\] . \' try to upload

5.           file(s).\';

6.  }

7.  

8.  \$folderName = date(\"m.d.Y\");

9.  if (!is_dir(\'upload/\'.\$folderName)) {

10.     mkdir(\'upload/\'.\$folderName);

11. }

12. 

13. \$fn = (isset(\$\_SERVER\[\'HTTP_X_FILENAME\'\]) ? \$\_SERVER\[\'HTTP_X_FILENAME\'\] :

14.                                             false);

15. if (\$fn)

16. {

17.     file_put_contents(\'upload/\' . \$folderName . \'/\' . \$fn,   
     

18.                       file_get_contents(\'php://input\'));

19.     echo \"\$fn uploaded\";

20.     exit();

21. }

22. else {

23.  
     if (isset(\$\_FILES) && is_array(\$\_FILES) && array_key_exists(\'formFiles\',

24.                                               \$\_FILES)) {

25.      
    \$number_files_send = count(\$\_FILES\[\'formFiles\'\]\[\'name\'\]);

26.       \$dir = realpath(\'.\') . \'/upload/\' . \$folderName . \'/\';

27. 

28.       if (\$number_files_send \> 0) {

29.          for (\$i = 0; \$i \< \$number_files_send; \$i++) {

30.             echo \'\<br/\>Reception of :
    \' . \$\_FILES\[\'formFiles\'\]\[\'name\'\]\[\$i\];

31.            
    \$copy = move_uploaded_file(\$\_FILES\[\'formFiles\'\]\[\'tmp_name\'\]

32.                    
    \[\$i\], \$dir . \$\_FILES\[\'formFiles\'\]\[\'name\'\]\[\$i\]);

33.             if (\$copy) {

34.               echo \'\<br /\>File
    \' . \$\_FILES\[\'formFiles\'\]\[\'name\'\]\[\$i\] .

35.                    \' copy\';

36.             }

37.             else {

38.               echo \'\<br /\>No file to upload\';

39.             }

40.         }

41.      }

42.    }

43. }

44. 

45. ?\>

## 3.5.5 Discussion

Here is the discussion forum for this part of the course.

### Suggested topics of discussion:

-   The given examples come with PHP code. If you adapt them to work
    with another server side languages, please share!

-   There are many possible improvements to the provided examples in the
    client code: monitoring the speed of upload/downloads, canceling an
    upload, etc. The examples are given \"as is\"\... if you improve
    them, as usual, share them in the forum!

## 3.6.1 Concepts (part 1)

Hello everyone! Today I will talk about IndexedDB.

In this first video, we will present the main concepts of this
client-based NoSQL database.

IndexedDB is a front-end database. It means that it runs directly in
your browser contrarily to

MySQL, Postgres or Oracle databases that run on the server side.

In our case, we\'ve got a NoSQL database, it means that we will not be
able to use SQL.

And in the NoSQL world of databases, we will find different kinds of
databases\...

Some use graph representations, some use object representations.

In our case, we will store directly JavaScript objects.

Here is an example; in this case, you\'ve got a person defined by two
properties:

firstName and lastName. It is designed to work with huge amount of

data with also very good performances. You can use indexes. So an index
system allows

you to specify that some properties will be 'indexes' and this will make
requests on these

properties much faster. For example, if I\'ve got 100 000 people in my

database, and I am looking for all the people with the last name equal
to 'Buffa'.

If the lastName is an index, the retrieval will be very very fast.

And also, remember that in the JavaScript world, all operations are
asynchronous.

So we will see in the next video that we will that we use callbacks
everywhere.

You open a video, you will need to check that it has been correctly
opened in a callback.

You insert data, you will need to check in a callback that the insert
has been performed correctly.

So databases, when you store objects inside

are called 'object stores', they have a name and they are attached to a
domain.

You can imagine they are attached to a Web app.

So let\'s look at some examples. The first very popular example is
Google Drive.

So Google Drive stores lots of documents, spreadsheets, presentations...
and if you are

offline, it works! So I just open the dev tools and you can see

that Google Drive relies a lot on IndexedDB. So we\'ve got different
data stores here and

the different data stores will hold, for example, the synced documents
I\'ve got in my repository.

And these documents are JavaScript objects, you can see the brackets
here that are typical

of JavaScript objects, and you have got properties like the data, the
viewMode and so on.

Another example is a guitar pedalboard I wrote for processing in real
time the

sound of the guitar. You can see that we have got different
categories...

and we can select different presets, and each preset is attached with
some values or a position...

and if I reload the application it remembers exactly the settings
because every time I am

doing an action, I am storing the current state in an IndexedDB
database, here\... and I

am storing directly JavaScript object with the preset values and so on.

And we are synchronizing this database that is located in the browser
with a MongoDB database

that is located on the server side and that holds also JavaScript
objects.

So having the same representation for data -JavaScript objects-, is
really comfortable.

So in the course, you will see a lot of small examples that we prepared
on JSBin, and each

of these examples show an individual operation, a very core operation
like creating a Customer database.

So if I click on the \"create CustomerDB database\" (button),

and if I open the devtools console, and I go to IndexedDB, I can see
that the CustomerDB

database I created appeared here, and I can see that the objects are
stored: people with an age,

email, name and a social security number. So you will see examples for
creating a database,

for working with data, for inserting data, removing data, modifying
data, getting data

and so on. And each of these small examples will provide

very useful code that you can reuse in your own examples.

In the course, you will also find more complete examples like this one
that shows how you can

make requests to collect just some subset of data using what we called
'bounds'.

So, for example, if you want to get just one single result, you can
interactively try this

application, or if you want all the data running from 'Batman' to
'Curry', you can also try this...

These examples should be good starting points for writing big scale
application.

In the next video, we will complete the presentation of the main
concepts, so see you there, bye!

IndexedDB is presented as an alternative to the WebSQL Database, which
the W3C deprecated on November 18, 2010 (while still available in some
browsers, it is no longer in the HTML5 specification). Both are
solutions for storage, but they do not offer the same functionalities.
WebSQL Database is *a relational database access system*,
whereas **IndexedDB is *an indexed table system***.

From [the W3C specification about
IndexedDB](https://www.w3.org/TR/IndexedDB/): \"*User agents (apps
running in browsers) may need to store large numbers of objects locally
in order to satisfy off-line data requirements of Web applications.
Where WebStorage (as seen in the HTML5 part 1 course -localStorage and
sessionStorage) is useful for storing pairs of keys and their
corresponding values, IndexedDB provides in-order retrieval of keys,
efficient searching of values, and the storage of duplicate values for a
key*\". 

The W3C specification provides a concrete API to perform advanced
key-value data management that is at the heart of most sophisticated
query processors. It does so by using *transactional databases* to store
keys and their corresponding values (one or more per key), and providing
a means of traversing keys in a deterministic order. This is often
implemented through the use of persistent B-tree data structures which
are considered efficient for insertion and deletion, as well as for
in-order traversal of very large numbers of data records.

**To sum up:**

1.  **IndexedDB is a transactional Object Store in which you will be
    able to store JavaScript objects.**

2.  **Indexes on some properties of these objects facilitate faster
    retrieval and search.**

3.  **Applications using IndexedDB can work both online and offline.**

4.  **IndexedDB is transactional: it manages concurrent access to
    data.**

#### Examples of applications where IndexedDB should be considered

![google drive uses
indexedDB](./images/image029.jpeg){width="3.28125in"
height="4.041666666666667in"}

-   A catalog of DVDs in a lending library.

-   Mail clients, to-do lists, notepads.

-   Data for games: high-scores, level definitions, etc.

-   Google Drive uses IndexedDB extensively\...

### External resources

Much of this chapter either builds on or is an adaptation of articles
posted on the Mozilla Developer Network (MDN) Web site
([IndexedDB](https://developer.mozilla.org/en-US/docs/IndexedDB), [Basic
Concepts of
IndexedDB](https://developer.mozilla.org/en-US/docs/IndexedDB/Basic_Concepts_Behind_IndexedDB) and [Using
IndexedDB](https://developer.mozilla.org/en-US/docs/IndexedDB/Using_IndexedDB)).

-   [W3C specification about
    IndexedDB](https://www.w3.org/TR/IndexedDB/)

-   [MDN\'s page about the IndexedDB
    API](https://developer.mozilla.org/en/IndexedDB)

-   [Getting Started with Persistent Offline Storage with
    IndexedDB](https://itnext.io/getting-started-with-persistent-offline-storage-with-indexeddb-1af66727246c)

[Current support is excellent](https://caniuse.com/#search=indexed) both
on mobile and desktop browsers.

## 3.6.2 Concepts (part 2)

Among the concepts used by IndexedDB is the concept of transactions.

A transactional database ensures that concurrent access to data would
not compromise this data.

It uses a locking system, that means that when an instance of your Web
application is modifying

some data and another instance or another application on the same domain
is reading this data, there won\'t be anything wrong regarding to this
data.

When do we need such a mechanism? When you have multiple tabs opened on
the same WebApp or WebApps from the same domain. Or you have got
multiple games that store high scores and they are all coming from
the\"MyBeautifulGame.com\" domain. They will share the same database

You need to have some security system. But remember also that HTML5 is
also used for writing applications that run outside of the traditional
browser, like on a game console...the PS4, the Xbox One\... your Windows
desktop uses also applications written in HTML5.

All these applications will belong to the same default domain and if
they need to store data, in an IndexedDB database -there is an IndexedDB
database in your Xbox or in your PlayStation-!

Then, in that case all these applications will have to fight for
accessing the data and you need transactions.

Another concept is called the KeyPath.

The KeyPath is like a unique ID attached to each data in your database.

And this KeyPath is either one explicit property, in that case the
social security number, it\'s a unique ID attached to each data in your
data store and it is called the KeyPath, it should be unique. It can be
explicit or implicit, if you do not specify any KeyPath when you create
your database another extra property will be added to your object. It\'s
a bit like the auto-incremented primary keys in the SQL world.

You can also have flexible schemas for your data.

All your data need to share the unique ID I just talked about, but they
can have some variable properties\... you can have some contacts for
example, in your data store, that have one single phone number or
multiple phone numbers, or a description, or an age, or a name attached
to them...

... but not all objects must share the same schema like what you have
got in relational tables in a relational databases. Another concept we
find in most databases

is the concept of 'indexes'. You can specify that a property of your
object you store in a database is an index. In that case, the retrieval
of data using this index will be much faster. And indexes, contrarily to
KeyPath, can be unique or non unique. For example if my object has a
lastName,

I can have several objects with lastName being Buffa, my family name,
and I can send a request

to the database asking for all the people whose lastName is equal to
Buffa.

And in that case, the retrieval will be much faster than if lastName was
not an index.

To sum up: IndexedDB is a NoSQL database, that stores JavaScript
objects. It runs in your browser (client side), it uses transactions -
so several tabs or several applications on the same domain can access
with a lot of security a same data at the same time.

It uses indexes for faster retrieval, and finally it can hold huge
amount of data.

Thanks for your attention, in the next videos we will look at some
pieces of code to learn how to program some application that will use
IndexedDB. Bye bye!

IndexedDB is very different from SQL databases, but don\'t be afraid if
you\'ve only used SQL databases: IndexedDB might seem complex at first
sight, but it really isn\'t.

Let\'s quickly look at the main concepts of IndexedDB, as we will go
into detail later on:

-   IndexedDB stores and retrieves objects which are indexed by a
    \"key\".

-   Changes to the database happen [within
    transactions](https://en.wikipedia.org/wiki/Database_transaction).

-   IndexedDB follows [a same-origin
    policy](https://www.w3.org/Security/wiki/Same_Origin_Policy). So
    while you can access stored data within a domain, you cannot access
    data across different domains.

-   It makes extensive use of an asynchronous API: most processing will
    be done in callback functions - and we mean *LOTS of callback
    functions*!

### Detailed overview

**IndexedDB databases store key-value pairs.** The values can be complex
structured objects (hint: think in terms of JSON objects), and keys can
be properties of those objects. You can create indexes that use any
property of the objects for faster searching, as well as ordering
results.

Example of data (we reuse a sample from this MDN tutorial: \"[Using
IndexedDB](https://developer.mozilla.org/en-US/docs/IndexedDB/Using_IndexedDB))\":

// This is what our customer data looks like.

const customerData = \[

{ ssn: \"444-44-4444\", name: \"Bill\", age: 35, email: \"bill@company.com\" },

{ ssn: \"555-55-5555\", name: \"Donna\", age: 32, email: \"donna@home.org\" }

\];

Where customerData is an array of  \"customers\", each customer having
several properties: ssn for the social security number, a name,
an age and an email address.

**IndexedDB is built on a transactional database model.** Everything you
do in IndexedDB happens in [the context of a
transaction](https://developer.mozilla.org/en-US/docs/IndexedDB/Basic_Concepts_Behind_IndexedDB#gloss_transaction).
The IndexedDB API provides lots of objects that represent indexes,
tables, cursors, and so on, but each is tied to a particular
transaction. Thus, you cannot execute commands or open cursors outside a
transaction.

### Example of a transaction:

1.  // Open a transaction for reading and writing on the DB \"customer\"

2.  var transaction = db.transaction(\[\"customers\"\], \"readwrite\");

3.  

4.  // Do something when all the data is added to the database.

5.  transaction.oncomplete = function(event) {

6.     alert(\"All done!\");

7.  };

8.  

9.  transaction.onerror = function(event) {

10.    // Don\'t forget to handle errors!

11. };

12. 

13. // Use the transaction to add data\...

14. var objectStore = transaction.objectStore(\"customers\");

15.  

16. for (var i in customerData) {

17.    var request = objectStore.add(customerData\[i\]);

18. 

19.    request.onsuccess = function(event) {

20.       // event.target.result == customerData\[i\].ssn

21. };

22. }

Transactions have a well-defined lifetime. Attempting to use a
transaction after it has completed throws an exception.

*Transactions auto-commit, and cannot be committed manually.*

This transaction model is really useful when you consider what might
happen if a user opened two instances of your web app in two different
tabs simultaneously. Without transactional operations, the two instances
might stomp all over each others\' modifications. 

**The IndexedDB API is mostly asynchronous.** The API doesn\'t give you
data by returning values; instead, you have to pass a callback function.
You don\'t \"store\" a value in the database, or \"retrieve\" a value
out of the database through synchronous means. Instead, you \"request\"
that a database operation happens. You are notified by a DOM event when
the operation finishes, and the type of event lets you know if the
operation succeeded or failed. This may sound a little complicated at
first, but there are some sanity measures baked-in. After all, you are a
JavaScript programmer, aren\'t you? ;-)

So, please review the previous code extracts noting: transaction.
oncomplete, transaction. onerror, request. onsuccess, etc.

**IndexedDB uses requests all over the place.** Requests are objects
that receive the success or failure DOM events mentioned previously.
They have onsuccess and onerror properties, and you can
call addEventListener() and removeEventListener() on them. They also
have readyState, result, and errorCode properties which advise the
status of a request.

The result property is particularly magical, as it can be many different
things, depending on how the request was generated (for example,
an IDBCursor instance, or the key for a value that you just inserted
into the database). We will see this in detail during a future lecture:
\"Using IndexedDB\".

**IndexedDB uses DOM events to notify you when results are
available.** DOM events always have a type property (in IndexedDB, it is
most commonly set to \"success\" or \"error\"). DOM events also have
a target property that shows where the event is headed. In most cases,
the target of an event is the IDBRequest object that was generated as a
result of doing some database operation. Success events don\'t bubble up
and they can\'t be cancelled. Error events, on the other hand, do
bubble, and can be cancelled. This is quite important, as error events
abort the transaction, unless they are cancelled.

**IndexedDB is object-oriented**. IndexedDB is not a relational
database, which has tables with collections of rows and columns. This
important and fundamental difference affects the way you design and
build your applications. IndexedDB is an Object Store!

In a traditional relational data store, you would have a table that
stores a collection of rows of data and columns of named types of data.
IndexedDB, on the other hand, requires you to create an object store for
a type of data and simply persist JavaScript objects to that store. Each
object store can have a collection of indexes (corresponding to the
properties of the JavaScript object you store in the store) that enable
efficient querying and iteration.

**IndexedDB does not use Structured Query Language (SQL).** It phrases a
query in terms of an index, that produces a cursor, which you use to
iterate through the result set. If you are not familiar with NoSQL
systems, read [the Wikipedia article on
NoSQL](https://en.wikipedia.org/wiki/NoSQL).

**IndexedDB adheres to a same-origin policy.** An origin consists of the
domain, the application layer protocol, and the port of a URL of the
document where the script is being executed. Each origin has its own
associated set of databases. Every database has a name that identifies
it within an origin. Think of it as: \"an application + a Database\".

The concept of \"same origin\" is defined by the combination of all
three components mentioned earlier (domain, protocol, port). For
example, an app in a page with the URL https://www.example.com/app/, and
a second app at https://www.example.com/dir/, may both access the same
IndexedDB database because they have the *same origin* (https,
example.com, and 80). Whereas apps at https://www.example.com:8080/dir/
(different port) or https://www.example.com/dir/ (different protocol),
do not satisfy the *same origin* criteria (port or protocol differ
from https://www.example.com)

See this article from MDN about [the same-origin
policy](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy) for
further details and examples.

## 3.6.3 Definitions

> This chapter can be read as is, but it is primarily given as a
> reference. We recommend you skim read it, then do the next section
> (\"using IndexedDB\"), then come back to this page if you need any
> clarification.

These definitions come from [the W3C
specification](https://www.w3.org/TR/IndexedDB/#database-api). Please
read this page to familiarize yourself with the terms.

### Database

-   Each [origin](https://www.w3.org/TR/IndexedDB/#dfn-origin) (you may
    consider as \"each application\") has an associated set
    of [databases](https://www.w3.org/TR/IndexedDB/#dfn-database).
    A *database* comprises one or more [object
    stores](https://www.w3.org/TR/IndexedDB/#dfn-object-store) which
    hold the data stored in the database.

-   Every database has a *name* that identifies it within a specific
    origin. The name can be any string value, including the empty
    string, and stays constant for the lifetime of the database.

-   Each database also has a current version. When a database is first
    created,
    its [version](https://www.w3.org/TR/IndexedDB/#dfn-version) is 0, if
    not specified otherwise.  Each database can only have one version at
    any given time. A database can\'t exist in multiple versions at
    once.

-   The act of opening a database creates *a connection*. There may be
    multiple [connections](https://www.w3.org/TR/IndexedDB/#dfn-connection) to
    a given database at any given time.

### Object store

-   An object store is the mechanism by which data is stored in the
    database. 

-   Every object store has *a name*. The name is unique within the
    database to which it belongs.

-   The object store persistently holds records (JavaScript objects),
    which are key-value pairs. One of these keys is  a kind of \"primary
    key\" in the SQL database sense. This \"key\" is a property that
    every object in the datastore *must* contain. Values in the object
    store are structured, but this structure may vary between objects
    (i.e., if we store persons in a database, and use the email as \"the
    key all objects must define\", some may have first name and last
    name, others may have an address or no address at all, etc.)

-   Records within an object store are sorted according
    to [keys](https://developer.mozilla.org/en-US/docs/IndexedDB/Basic_Concepts_Behind_IndexedDB#gloss_key), in
    ascending order.

-   Optionally, an object store may also have a* [key
    generator](https://www.w3.org/TR/IndexedDB/#dfn-key-generator) *and
    a [*key
    path*](https://www.w3.org/TR/IndexedDB/#dfn-object-store-key-path).
    If the object store has a key path, it is said to use in-line keys.
    Otherwise, it is said to use *out-of-line* keys.

-   The object store can derive [the
    key](https://www.w3.org/TR/IndexedDB/#key-construct) from one of
    three sources:

    1.  A key generator. A key generator generates a monotonically
        increasing number every time a key is needed. This
        is somewhat similar to auto-incremented primary keys in a SQL
        database.

    2.  Keys can be derived via a key path.

    3.  Keys can also be explicitly specified when [a
        value](https://www.w3.org/TR/IndexedDB/#value-construct) is
        stored in the object store.s

Further details will be given in the next chapter \"Using IndexedDB\".

### Version

-   When a database is first created, its version is the integer 0. Each
    database has one version at a time; a database can\'t exist in
    multiple versions at once.

-   The only way to change the version is by opening it with a higher
    version number than the current one. This will start
    a versionchange transaction and fire an upgradeneeded event. The
    only place where the schema of the database can be updated is inside
    the handler of that event.

This definition describes[ the most recent
specification](https://w3c.github.io/IndexedDB/), which is only
implemented in up-to-date browsers. Old browsers implemented the now
deprecated and removed IDBDatabase.setVersion() method.

### Transaction

From the specification: \"*A transaction is used to interact with the
data in a database. Whenever data is read or written to the database,
this is done by using [a
transaction](https://www.w3.org/TR/IndexedDB/#dfn-transaction).*

*All transactions are created through [a
connection](https://www.w3.org/TR/IndexedDB/#dfn-connection), which is
the transaction\'s connection. The transaction has [a
mode](https://www.w3.org/TR/IndexedDB/#dfn-mode) (read, readwrite or versionchange)
that determines which types of interactions can be performed upon that
transaction. The mode is set when the transaction is created and remains
fixed for the life of the transaction. The transaction also has a scope
that determines the object stores with which the transaction may
interact*.\"

A transaction in IndexedDB is similar to a transaction in a SQL
database. It defines: \"*An atomic and durable set of data-access and
data-modification operations*\". Either all operations succeed or all
fail. 

A database connection can have several active transactions associated
with it at a time, but these write transactions cannot have
overlapping [scopes](https://developer.mozilla.org/en-US/docs/IndexedDB/Basic_Concepts_Behind_IndexedDB#scope) (*they
cannot work on the same data at the same time*). The scope of a
transaction, which is defined at creation time, determines which
concurrent transactions can read or write the same data (multiple reads
can occur, while writes will be sequential, only one at a time), and
remains constant for the lifetime of the transaction.

So, for example, if a database connection already has a writing
transaction with a scope that covers only the flyingMonkey object store,
you can start a second transaction with a scope of
the unicornCentaur and unicornPegasus object stores. As for reading
transactions, you can have several of them, and they may even overlap. A
\"versionchange\" transaction never runs concurrently with other
transactions (reminder: we usually use such transactions when we create
the object store or when we modify the schema).

Generally speaking, the above requirements mean that \"readwrite\"
transactions which have overlapping scopes always run in the order they
were [created](https://www.w3.org/TR/IndexedDB/#dfn-transaction-create),
and never run in parallel. A \"versionchange\" transaction is
automatically created when a database version number is provided that is
greater than the current database version. This transaction will be
active inside the onupgradeneeded event handler, allowing the creation
of new object stores
and [indexes](https://www.w3.org/TR/IndexedDB/#dfn-index).

### Request

The operation by which reading and writing on a database is done. Every
request represents one read or one write operation. Requests are always
run within a transaction. The example below adds a customer to the
object store named \"customers\".

1.  // Use the transaction to add data\...

2.  var objectStore = transaction.objectStore(\"customers\");

3.  for (var i in customerData) {

4.      **var request = objectStore.add(customerData\[i\]);**

5.      **request.onsuccess **= function(event) {

6.          // event.target.result == customerData\[i\].ssn

7.  };

8.  }

### Index

It is sometimes useful to
retrieve [records](https://www.w3.org/TR/IndexedDB/#dfn-record) from an
object store through means other than their key.

An *index* allows the user to look up records in an object store using
the properties of the values in the object store\'s records. Indexes are
a common concept in databases. Indexes can speed up object retrieval and
allow multi-criteria searches. For example, if you store persons in your
object store, and add an index on the \"email\" property of each person,
then searching for some person using his/her email address will be much
faster.

An index is a specialized persistent key-value storage and has
a *referenced* object store. For example, with our \"persons\" object
store, that is the referenced data store. Then, a reference store may
have an index store associated with it, that contains indexes which map
email values to key values in the reference store (for example).

An index is *a list of records* which holds the data stored in the
index. The records in an index are automatically populated whenever
records in [the referenced object
store](https://www.w3.org/TR/IndexedDB/#dfn-referenced) are inserted,
updated or deleted. There may be several indexes referencing the same
object store, in which case changes to the object store cause all such
indexes to update.

An index contains *a unique flag*. When this flag is set to true, the
index enforces the rule that no two records in the index may have the
same key. If a user attempts to insert or modify a record in the
index\'s referenced object store, such that an indexed attribute\'s
value already exists in an index, then the attempted modification to the
object store fails.

### **Key and values**

#### Key

A data value by which stored values are organized and retrieved in the
object store. The object store can derive the key from one of three
sources: [a key
generator](https://developer.mozilla.org/en-US/docs/IndexedDB/Basic_Concepts_Behind_IndexedDB#gloss_keygenerator), [a
key
path](https://developer.mozilla.org/en-US/docs/IndexedDB/Basic_Concepts_Behind_IndexedDB#gloss_keypath),
and an explicitly specified value.

The key must be of a data type that has a number that is greater than
the one before. Each record in an object store must have a key that is
unique within the same store, so you cannot have multiple records with
the same key in a given object store.

**A key can be one of the following
types: [string](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/String), [date](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Date), float, **and** [array](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Array)**.
For arrays, the key can range from an empty value to infinity. And you
can include an array within an array.

Alternatively, you can also look up records in an object store
using [ an
index](https://developer.mozilla.org/en-US/docs/IndexedDB/Basic_Concepts_Behind_IndexedDB#gloss_index).

#### Key generator

A mechanism for producing new keys in an ordered sequence. If an object
store does not have a key generator, then the application must provide
keys for records being stored. Similar to auto-generated primary keys in
SQL databases.

#### In-line key

A key that is stored as part of the stored value. Example: the email of
a person or a student number in an object representing a student in a
student store. It is found using *a key path*. An in-line key could be
generated using a generator. After the key has been generated, it can
then be stored in the value using the key path, or it can also be used
as a key.

#### Out-of-line key

A key that is stored separately from the value being stored, for
instance, an auto-incremented id that is not part of the object.
Example: you store persons {name:Buffa,
firstName:Michel} and {name:Forgue, firstName: Marie}, each will have a
key (think of it as a primary key, an id\...) that can be auto-generated
or specified, but that is not part of the object stored.

#### Key path

Defines where the browser should extract the key from a value in the
object store or index. **A valid key path can include one of the
following: an empty string, a JavaScript identifier, or multiple
JavaScript identifiers separated by periods. It cannot include spaces.**

#### Value

Each record has a value, which could include anything that can be
expressed in JavaScript,
including: [boolean](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Boolean), [number](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Number), [string](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/String), [date](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Date), [object](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Object), [array](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Array), [regexp](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/RegExp), [undefined](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/undefined),
and null.

When an object or an array is stored, the properties and values in that
object or array can also be anything that is a valid value.

Blobs and files can be stored, (supported by all major browsers, IE \>
9). The example in the next chapter stores images using blobs.

### **Range and scope**

#### Scope

The set of object stores and indexes to which a transaction applies. The
scopes of read-only transactions can overlap and execute at the same
time. On the other hand, the scopes of writing transactions cannot
overlap. You can still start several transactions with the same scope at
the same time, but they just queue up and execute one after another.

#### Cursor

A mechanism for iterating over multiple records within a *key range*.
The cursor has a source defining which index or object store it is
iterating. It has a position within the range, and retrieves records
sequentially according to the value of their keys in either increasing
or decreasing order. For the reference documentation on cursors,
see IDBCursor.

#### Key range

A continuous interval over some data type used for keys. Records can be
retrieved from object stores and indexes using keys or a range of keys.
You can limit or filter the range using lower and upper bounds. For
example, you can iterate over all the values of a key between x and y.

For the reference documentation on key range, see IDBKeyRange.

## 3.6.4 Using IndexedDB

This page and the following one, entitled \"Using IndexedDB\",
provide simple examples for creating, adding, removing, updating, and
searching data in an IndexedDB database. They explain the basic steps to
perform such common operations, while explaining the
programming principles behind IndexedDB.

**In the \"Using IndexedDB\" pages of this course, you will learn
about:**

-   Creating and populating a database

-   Working with data

-   Using transactions

-   Inserting, deleting, updating and getting data

-   Creating and populating a database

### External resources

Additional information is available on these Web sites. Take a look at
these!

-   MDN\'s documentation on \"[Using
    IndexedDB](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API/Using_IndexedDB)\"

-   [Storing images and files in
    IndexedDB](http://robertnyman.com/2012/03/06/storing-images-and-files-in-indexeddb/)

-   [Working with
    IndexedDB](https://developers.google.com/web/ilt/pwa/working-with-indexeddb)

-   [How to view IndexedDB content in
    Firefox](https://stackoverflow.com/questions/9846013/how-to-view-indexeddb-content-in-firefox)

## 3.6.5 Creating and deleting a database

Hi! Let\'s look now at some pieces of code and examples that will
explain how to really program an IndexedDB application.

So... one of the first thing is that you need

to create or to open an existing database before working with data.

All operations are asynchronous and, if you want to open a database, you
use IndexedDB.open(...).

You specify the name of the database and the version. Each database is
versioned\... and

if the \"CustomerDB\" database -from this example- exists with a version
\"2\", it will

just open it. If it exists, but with a previous, lower version, it will
be \"upgraded\".

This is why we need to define, on the object that is returned by
open(\...), some event listeners.

The \"onsuccess\" listener is called when the database has been opened.
\"onerror\" (listener)

if there is an error, and \"onupgradeneeded\" (listener) will be called
only if we are creating

a new version of the database. It\'s the case when the database does not
exist.

So the database has a version, and the first version is \"0\". You can
have the same database that

exists in different versions at a time, but the very common way is to
define the two listeners I talked about,

and create the database and the schema in the \"onupgradeneeded\" event
listener.

And work with data on the \"onsuccess\" listener... because when you
enter in the \"onsuccess »,

it means that the database exists.

Be careful because on the Web you will find lots and lots of old
tutorials that use a

previous, deprecated version of the API. You can identify that if it
uses the setVersion()

method on an object called IDBDatabase. In that case look for a more
recent tutorial!

Here is an example of a database creation: you indicate a name\...
\"customerDB\",

you try to open it with version \"2\", and if the database does not
exist, you will enter

the \"onupgradeneeded\" listener. If it exists, you go to the
\"onsuccess\" listener.

The result (the event.target.result) will be the database itself. We
will work with this object for

inserting, deleting, modifying or looking for data.

Now, let\'s zoom a little bit on what happens in this listener here,
because this is where

we are going to create the database.

For creating and populating a new object datastore - a new object
database -, here is how we proceed:

in the \"onupgradeneeded\" listener, we get the database itself\... Then
you create an object

store in it, and you need to indicate the name of the object store -
\"customers\" - and

the name of the \"KeyPath\". Remember, the KeyPath is a unique ID that
will be attached

to all objects stored in the database (!: correction -\> datastore).

And we can also create \"indexes\". Here, we are saying that every
object that will be stored

in the database (!: correction -\> datastore), will have a property
called \"name\", that will

not be necessarily unique, and we will have a property called \"email\"
that will be unique.

Just after creating it, we are populating the objectstore with some test
data. Here we

are iterating on the customerData object, that has been defined here.
It\'s an array,

that contains two persons (two customers) inside: one is \"Bill\", age
35, with an email and a

unique ID that is its social security number. Let\'s try this one: it
comes from

the example called \"creating and deleting a database\". I open it, I
open the devtools,

and I look at \"Resources\" (tab). I open the \"IndexedDB\" (item). You
can see that the

datastore and the database are not present here. I click on the \"create
customer database\" ...

this will run the code I just explained. And if I refresh the IndexedDB,

I can see that the database called \"CustomerDB\" has been created, with
inside

an object store called \"customers\", that contains two persons (two
customers), and I can see

here the indexes. I can open also the objects. If I want to delete the
database, I can do

it in my own program, or I can do it in the console. I run
IndexedDB.deleteDatabase(\...),

and I indicate the database - \"customerDB\" - . If I go back to the
\"Resources\" tab, and

refresh the databases, heu.. if I refresh IndexedDB (databases)
-sorry-\... normally,

ok I run it again\... normally, it disappears\... sometimes the refresh
does not work correctly,

but the database is really deleted.

### Creating a database

[Our online example at JSBin](https://jsbin.com/govuci) shows how to
create and populate an object store named \"CustomerDB\". This example
should work on both mobile and desktop versions of all major post-2012
browsers.

We suggest that you follow what is happening using Google
Chrome\'s developer tools. Other browsers offer equivalent means for
debugging Web applications that use IndexedDB.

With Chrome, please open the JSBin example and activate the Developer
tool console (F12 or cmd-alt-i). Open the JavaScript and HTML tabs on
JSBin.

Then, click the \"Create CustomerDB\" button in the HTML user interface
of the example: it will call the createDB() JavaScript function that:

1.  creates a new IndexedDB database and an object store in it
    (\"customersDB\"), and

2.  inserts two javascript objects (look at the console in your
    devtools - the Web app prints lots of traces in there, explaining
    what it does under the hood). Note that the social security number
    is the \"Primary key\", called *a key path* in the IndexedDB
    vocabulary (red arrow on the right of the screenshot).

**Chrome DevTools (F12 or cmd-alt-i) shows the IndexedDB databases,
object stores and data:**

![](./images/image030.png){width="6.5in"
height="4.778472222222222in"}

Normally, when you create a database for the first time, the console
should show this message:

![Message displayed in console when the database is created the first
time you run the
example](./images/image031.jpeg){width="6.5in"
height="0.825in"}

This message comes from the JavaScript request.onupgradeneeded callback.
Indeed, the first time we open the database we ask for a specific
version (in this example: version 2) with:

1.  var request = indexedDB.open(dbName, 2);

\...and if there is no version \"2\" of the database, then we enter
the onupgradeneeded callback where we actually create the database.

You can try to click again on the button \"CreateCustomerDatabase\", if
database version \"2\" exists, this time the request.onsuccess callback
will be called. This is where we will add/remove/search data (you should
see a message on the console).

Notice that the version number cannot be a float: \"1.2\" and \"1.4\"
will automatically be rounded to \"1\".

### JavaScript code from the example:

1.  var db; // the database connection we need to initialize

2.   

3.  function createDatabase() {

4.  

5.    if(!window.indexedDB) {

6.       window.alert(\"Your browser does not support a stable version

7.                     of IndexedDB\");

8.    }

9.  

10.   // This is what our customer data looks like.

11.   var customerData = \[

12.     { ssn: \"444-44-4444\", name: \"Bill\", age: 35, email:

13.                                            \"bill@company.com\" },

14.     { ssn: \"555-55-5555\", name: \"Donna\", age: 32, email:

15.                                            \"donna@home.org\" }

16.   \];

17.   var dbName = \"CustomerDB\";

18. 

19.   // version must be an integer, not 1.1, 1.2 etc\...

20.   var request = indexedDB.open(dbName, 2);

21. 

22.   request.onerror = function(event) {

23.      // Handle errors.

24.      console.log(\"request.onerror
    errcode=\" + event.target.error.name);

25.   };

26.   request.onupgradeneeded = function(event) {

27.       console.log(\"request.onupgradeneeded, we are creating a

28.                    new version of the dataBase\");

29. 

30.       db = event.target.result;

31. 

32.       // Create an objectStore to hold information about our

33.       // customers. We\'re going to use \"ssn\" as our key path
    because

34.       //  it\'s guaranteed to be unique

35.       var objectStore = db.createObjectStore(\"customers\",

36.                                              
     { keyPath: \"ssn\" });

37. 

38.       // Create an index to search customers by name. We may have  
             

39.       // duplicates so we can\'t use a unique index.

40.      
    objectStore.createIndex(\"name\", \"name\", { unique: false });

41. 

42.       // Create an index to search customers by email. We want to

43.       // ensure that no two customers have the same email, so use a

44.       // unique index.

45.      
    objectStore.createIndex(\"email\", \"email\", { unique: true });

46. 

47.       // Store values in the newly created objectStore.

48.       for (var i in customerData) {

49.           objectStore.add(customerData\[i\]);

50.       }

51.   }; // end of request.onupgradeneeded

52. 

53.   request.onsuccess = function(event) {

54.      // Handle errors.

55.      console.log(\"request.onsuccess, database opened, now we can
    add

56.                   / remove / look for data in it!\");

57. 

58.      // The result is the database itself

59.      db = event.target.result;

60.   };

61. } // end of function createDatabase

### **Explanations:**

All the \"creation\" process is done in the onupgradeneeded callback
(*lines 26-50*):

-   *Line 30*: get the database created in the result of the dom
    event: db = event.target.result;

-   *Line 35*: create an object store named \"customers\" with the
    primary key being the social security number (\"ssn\" property of
    the JavaScript objects we want to store in the object store): var
    objectStore = db.createObjectStore(\"customers\", {keyPath:
    \"ssn\"});

-   *Lines 39 and 44*: create indexes on the \"name\" and \"email\"
    properties of JavaScript objects: objectStore.createIndex(\"name\",
    \"name\", {unique: false});

-   *Lines 48-50*: populate the database: objectStore.add(\...).

> Note that we did not create any transaction, as
> the onupgradeneeded callback on a create database request is always in
> a default transaction that cannot overlap with another transaction at
> the same time.

If we try to open a database version that exists, then
the request.onsuccess callback is called. This is where we are going to
work with data. The DOM event result attribute is the database itself,
so it is wise to store it in a variable for later use: db=
event.target.result;

### Deleting a database

You can delete a database simply by running this command: 

indexedDB.deleteDatabase(\"databaseName\");

A common practice, while learning how IndexedDB works, is to type this
command in the devtool console. For example, we can delete the
CustomerDB database used in all examples of this course section by
opening one of the JsBin examples , then opening the devtool console,
then executing indexedDB.deleteDatabase(\"CustomerDB\"); in the console:

![deleting indexed DB part 1, open the devtool
console](./images/image032.jpeg){width="6.5in"
height="4.488888888888889in"}

![Run the command](./images/image033.jpeg){width="6.5in"
height="3.3409722222222222in"}

![Execute the command](./images/image034.jpeg){width="6.5in"
height="1.4131944444444444in"}

![Refresh IndexedDB display of
objectStores](./images/image035.jpeg){width="6.5in"
height="2.332638888888889in"}

![Final result: the objectStore has been
deleted](./images/image036.jpeg){width="6.5in"
height="1.84375in"}

## 3.6.6 Working with data

Explicit use of a transaction is necessary:

> **All operations in the database should occur within a transaction!**

While the creation of the database occurred in a transaction that ran
\"under the hood\" without explicit use of the \"transaction\"
keyword, **for adding/removing/updating/retrieving data, explicit use of
a transaction is required.**

We generate a transaction object from the database, indicate with which
object store the transaction will be associated, and specify an access
mode .

Source code example for creating a transaction associated with the
object store named \"customers\":

1.  **var transaction = db.transaction(\[\"customers\"\], \"readwrite\");** //
    or \"read\"\...

Transactions, when created, must have a mode set that is
either readonly, readwrite or versionchange (this last mode is only for
creating a new database or for modifying its schemas: i.e. changing the
primary key or the indexes).

> When you can, use readonly mode. Concurrent read transactions will
> become possible.

In the following pages, we will explain how to insert, search, remove,
and update data. A final example that merges all examples together will
also be shown at the end of this section.

## 3.6.7 Inserting data

So, about inserting data... Here this is what we did during the creation
of the database.

We used objectStore.add(\...). This is a particular case because when we
are creating the database,

nobody can do the same operation at the same time. So we don\'t need to
protect the insertion

of the data by a transaction. But usually, when you insert data, you
need

to create a transaction. This is what is done here: we create a
transaction on the dataStore

called \"customers », and we are indicating that we are going to read
data, and also write

data. You need to have listeners -callbacks- in case there is an error
during the creation

of the transaction. Then, if everything went ok, and using this object
store transaction,

you will add data. The fact that we are using the transaction here,
means that if somebody

is trying to access the same data (at the same time), somebody will have
to wait until

the other one finished its operation. In case of success, you need to
make callbacks,

on the request this time - on the add request. We can display \"ok,
customer with the social

serial (security) number has been added\", or we display an error.

Here, I shortened the error messages. In the course Web page the code is
more complete.

Here, the code is rather long... it takes 20 lines of code, but you
shorten this by

using the \".\" operator and with chaining requests (operations). You
create a transaction on the database,

then you create the same transaction on the object store, and you add,
with a request, a new customer.

This is much more concise, much shorter, but you cannot spot

with a lot of precision, the errors that can come. Is it an error during

this operation? During the transaction? When you try to open the
database in read / write

mode? You don\'t know!

Deleting data is really similar. So, the only thing that changes is the
name here,

of the operation you do on the request transaction. So, if you do a
\"delete\", and specify the

KeyPath of the data you want to delete, then it will delete the object
with social serial

(security) number 444., blah blah blah...

For modifying data it\'s the same thing: you use the \"put\" method on

the transaction, but this time you need to indicate an object -a
JavaScript object- whose

social security number -whose KeyPath- is valid: if this object exists
in the database

(datastore), we will update the new age for this customer.

Looking for data: you can look for a given data using \"get\" on the
transaction. In the

request, you specify the KeyPath... and in case of success the result
(the event.target.result)

that is passed to the callback, to the \"onsuccess\" callback, will be
the complete object whose key (KeyPath) is 1234 blah blah blah.

Getting more than one piece of data will be performed using a concept
called \"cursors\".

If we are looking for more than one result... in this example, we are
looking for multiple

results, then instead of having an \"onsuccess\" callback, you\'ve got
an objectStore.openCursor().onsuccess

And in that case, what you\'ve got as a result is a \"cursor\". A cursor
is like

a pointer on a collection of results, and by calling cursor.continue(),
you will go

from one result to the next one. And the cursor itself is the object,
the \"current\" object.

So, if we\'re getting a collection, then the current cursor.key, the
current cursor.value.name,

the current cursor.value.age, will be the values from the data you
retrieved, and by calling

cursor.continue(), you go to the next result. When the cursor is
\"null\" then there is no

more entries and you finish processing all your results.

You can also use indexes. Instead of using the \"get\" method, you first
indicate which

index you are going to use for getting data, on the objectStore
transaction you call a

method called \"index(...) », and you pass as a parameter the index
name. Then, on the

index itself, you do a \"get(\...)\". In that case it means \"please,
look for data whose

name is equal to Bill, and the name is an index!\". In that case, in the
callback, the

event.target.result is the resulting data you\'ve just looked for.

You can also look for more than one result. In that case, you do just
\"index.openCursor().onsuccess\"...

instead of \"index.onsuccess\" and you will get a collection of data.
The cursor will

point to the current data (in the collection). Then you iterate using
cursor.continue(),

on the collection of results, exactly the same way we explained earlier
with the previous

case when we got multiple results, this time it wasn\'t using an index.

### Example #1: basic steps

[Online example at JSBin](https://jsbin.com/jukifo):

Execute this example and look at the IndexedDB object store content from
the Chrome dev tools (F12 or cmd-alt-i). One more customer should have
been added.

**Be sure to click on the \"create database\" button before clicking the
\"insert new customer\" button.**

![example on JsBin for inserting data in
IndexedDB](./images/image037.png){width="6.5in"
height="2.816666666666667in"}

The next screenshot shows the IndexedDB object store in Chrome dev.
tools (use the \"Resources\" tab). Clicking the \"Create CustomerDB\"
database creates or opens the database, and clicking \"Add a new
Customer\" button adds a customer named \"Michel Buffa\" into the object
store:

![Devtools show that a new customer named Michel Buffa has been
inserted](./images/image038.png){width="6.5in"
height="3.533333333333333in"}

**Code from the example, explanations:**

We just added a single function into the example from the previous
section - the function AddACustomer() that adds one customer:

1.  **{ ssn: \"123-45-6789\", name: \"Michel Buffa\", age: 47, email:** 
     **\"buffa@i3s.unice.fr\" }**

Here is the complete source code of the addACustomer function:

1.  function addACustomer() {

2.     // 1 - get a transaction on the \"customers\" object store

3.     // in readwrite, as we are going to insert a new object

4.   
     var transaction = db.transaction(\[\"customers\"\], \"readwrite\");

5.  

6.     // Do something when all the data is added to the database.

7.     // This callback is called after transaction has been completely

8.     // executed (committed)

9.     transaction.oncomplete = function(event) {

10.        alert(\"All done!\");

11.    };

12. 

13.    // This callback is called in case of error (rollback)

14.    transaction.onerror = function(event) {

15.       console.log(\"transaction.onerror
    errcode=\" + event.target.error.name);

16.    };

17. 

18.    // 2 - Init the transaction on the objectStore

19.    var objectStore = transaction.objectStore(\"customers\");

20. 

21.    // 3 - Get a request from the transaction for adding a new object

22.    var request = objectStore.add({ ssn: \"123-45-6789\",

23.                                    name: \"Michel Buffa\",

24.                                    age: 47,

25.                                    email: \"buffa@i3s.unice.fr\" });

26. 

27.    // The insertion was ok

28.    request.onsuccess = function(event) {

29.        console.log(\"Customer with ssn=
    \" + event.target.result + \"

30.                     added.\");

31.    };

32. 

33.    // the insertion led to an error (object already in the store,

34.    // for example)

35.    request.onerror = function(event) {

36.        console.log(\"request.onerror, could not insert customer,

37.                     errcode = \" + event.target.error.name);

38.    };

39. }

**Explanations:**

In the code above, *lines 4, 19 and 22* show the main calls you have to
perform in order to add a new object to the store:

1.  Create a transaction.

2.  Map the transaction onto the object store.

3.  Create an \"add\" request that will take part in the transaction.

The different callbacks are in *lines 9 and 14* for the transaction, and
in *lines 28 and 35* for the request.

You may have several requests for the same transaction. Once all
requests have finished, the transaction.oncomplete callback is called.
In any other case the transaction.onerror callback is called, and the
datastore remains unchanged.

Here is the trace from the dev tools console:

![Trace from the devtools
console](./images/image039.png){width="6.5in"
height="1.238888888888889in"}

### Example #2: adding a form and validating inputs

[Online example available at JSBin](https://jsbin.com/jayida):

![a form has been added to the previous example, for creating a new
customer](./images/image040.jpeg){width="6.5in"
height="1.5027777777777778in"}

You can try this example by following these steps:

1.  Press first the \"Create database\" button

2.  then add a new customer using the form

3.  click the \"add a new Customer\" button

4.  then press F12 or cmd-alt-i to use the Chrome dev tools and inspect
    the IndexedDB store content. Sometimes it is necessary to refresh
    the view (right click on IndexedDB/refresh), and sometimes it is
    necessary to close/open the dev. tools to have a view that shows the
    changes (press F12 or cmd-alt-i twice). Chrome dev. tools are a bit
    strange from time to time.

This time, we added some tests for checking that the database is open
before trying to insert an element, and we added a small form for
entering a new customer.

Notice that the insert will fail and display an alert with an error
message if:

-   The ssn is already present in the database. This property has been
    declared as the keyPath (a sort of primary key) in the object store
    schema, and [it should be
    unique]{.underline}: db.createObjectStore(\"customers\", { keyPath:
    \"ssn\" });

-   The email address is already present in the object store. Remember
    that in our schema, the email property is an index that we declared
    as unique: objectStore.createIndex(\"email\", \"email\", { unique:
    true });

-   Try to insert the same customer twice, or different customers with
    the same ssn. An alert like this should pop up:

![insert
error](./images/image041.jpeg){width="6.083333333333333in"
height="2.3229166666666665in"}

**Here is the updated version of the HTML code of this example:**

1.  \<fieldset\>

2.    SSN: \<input type=\"text\" id=\"ssn\" placeholder=\"444-44-4444\"

3.                required/\>\<br\>

4.    Name: \<input type=\"text\" id=\"name\"/\>\<br\>

5.   
    Age: \<input type=\"number\" id=\"age\" min=\"1\" max=\"100\"/\>\<br\>

6.    Email:\<input type=\"email\" id=\"email\"/\> reminder, email must
    be

7.                 unique (we declared it as a \"unique\" index)\<br\>

8.  \</fieldset\>

9.  

10. \<button **onclick=\"addACustomer();\"**\>Add a new
    Customer\</button\>

**And here is the new version of the addACustomer() JavaScript
function:**

1.  function addACustomer() {

2.     if(db === null) {

3.        alert(\'Database must be opened, please click the Create

4.               CustomerDB Database first\');

5.        return;

6.     }

7.  

8.   
     var transaction = db.transaction(\[\"customers\"\], \"readwrite\");

9.  

10.    // Do something when all the data is added to the database.

11.    transaction.oncomplete = function(event) {

12.      console.log(\"All done!\");

13.    };

14. 

15.    transaction.onerror = function(event) {

16.      console.log(\"transaction.onerror
    errcode=\" + event.target.error.name);

17.    };

18. 

19.    var objectStore = transaction.objectStore(\"customers\");

20. 

21.    // adds the customer data

22.    var newCustomer={};

23.    newCustomer.ssn = document.querySelector(\"#ssn\").value;

24.    newCustomer.name = document.querySelector(\"#name\").value;

25.    newCustomer.age = document.querySelector(\"#age\").value;

26.    newCustomer.email = document.querySelector(\"#email\").value;

27.    alert(\'adding customer ssn=\' + newCustomer.ssn);

28.  

29.    var request = objectStore.add(newCustomer);

30. 

31.    request.onsuccess = function(event) {

32.      console.log(\"Customer with ssn= \" + event.target.result + \"

33.                   added.\");

34.      };

35.  

36.   request.onerror = function(event) {

37.      alert(\"request.onerror, could not insert customer, errcode =
    \"

38.            + event.target.error.name +

39.            \". Certainly either the ssn or the email is already

40.            present in the Database\");

41.   };

42. }

It is also possible to shorten the code of the above function by
chaining the different operations using the \".\" operator (getting a
transaction from the db, opening the store, adding a new customer,
etc.).

Here is the short version:

1.  var request = db.transaction(\[\"customers\"\], \"readwrite\")

2.  .objectStore(\"customers\")

3.  .add(newCustomer);

The above code does not perform all the tests, but you may encounter
such a way of coding (!).

Also, note that it works if you try to insert empty data:

![devtools show that inserting blank data
works](./images/image042.jpeg){width="6.5in"
height="2.688888888888889in"}

Indeed, entering an empty value for the keyPath or for indexes is a
valid value (in the IndexedDB sense). In order to avoid this, you should
add more JavaScript code. We will let you do this as an exercise.

## 3.6.8 Removing data

Let\'s move to the next [online example at
JSBin](https://jsbin.com/bavifa):

![devtools show that a customer has been removed once clicked on the
remove customer
button](./images/image042.jpeg){width="6.5in"
height="2.688888888888889in"}

See the changes in Chrome dev. tools: refresh the view (right
click/refresh) or press F12 or cmd-alt-i twice. There is a bug in the
refresh feature with some versions of Google Chrome.

How to try the example:

1.  Be sure to click the \"create database button\" to open the existing
    database.

2.  Then use Chrome dev tools  to check that the customer
    with ssn=444-44-444 exists. If it\'s not there, just insert into the
    database like we did earlier in the course.

3.  Right click on indexDB in the Chrome dev tools and refresh the
    display of the IndexedDB\'s content if necessary if you cannot see
    customer with ssn=444-44-444. Then click on the \"Remove Customer
    ssn=444-44-4444(Bill)\" button. Refresh the display of the database.
    The \'Bill\' object should have disappeared!

Code added in this example:

1.  function removeACustomer() {

2.     if(db === null) {

3.        alert(\'Database must be opened first, please click the

4.               Create CustomerDB Database first\');

5.        return;

6.     }

7.  

8.   
     var transaction = db.transaction(\[\"customers\"\], \"readwrite\");

9.  

10.    // Do something when all the data is added to the database.

11.    transaction.oncomplete = function(event) {

12.       console.log(\"All done!\");

13.    };

14. 

15.    transaction.onerror = function(event) {

16.       console.log(\"transaction.onerror errcode=\" +

17.                    event.target.error.name);

18.    };

19. 

20.    var objectStore = transaction.objectStore(\"customers\");

21. 

22.    alert(\'removing customer ssn=444-44-4444\');

23.    **var request = objectStore.delete(\"444-44-4444\");**

24. 

25.    request.onsuccess = function(event) {

26.       console.log(\"Customer removed.\");

27.    };

28. 

29.    request.onerror = function(event) {

30.       alert(\"request.onerror, could not remove customer, errcode

31.             = \" + event.target.error.name + \". The ssn does not

32.             exist in the Database\");

33.    };

34. }

Notice that after the deletion of the Customer (*line 23*),
the request.onsuccess callback is called. And if you try to print the
value of the event.target.result variable, it is \"undefined\".

**Short way of doing the delete:**

It is also possible to shorten the code of the above function a lot by
concatenating the different operations (getting the store from the db,
getting the request, calling delete, etc.). Here is the short version:

1.  var request = db.transaction(\[\"customers\"\], \"readwrite\")

2.  .objectStore(\"customers\")

3.  .delete(\"444-44-4444\");

## 3.6.9 Modifying data

We used request.add(object) to add a new customer
and request.delete(keypath) to remove a customer. Now, to modify data
from an object store with IndexedDB, we use request.put(keypath) to
update a customer!

[Online example at JSBin](https://jsbin.com/zugowe):

![devtools show a customer being updated in
IndexedDB](./images/image043.jpeg){width="6.5in"
height="3.4430555555555555in"}

The above screenshot shows how we added an empty customer with ssn=\"\",
(we just clicked on the open database button, then on the \"add a new
customer button\" with an empty form).

Now, we fill the name, age and email input fields to update the object
with ssn=\"\" and click on the \"update data about an existing
customer\" button. This updates the data in the object store, as shown
in this screenshot:

![devtools show updated
customer](./images/image044.jpeg){width="6.5in"
height="1.0819444444444444in"}

Here is the new code added to our example:

1.  function updateACustomer() {

2.     if(db === null) {

3.       alert(\'Database must be opened first, please click the Create

4.              CustomerDB Database first\');

5.       return;

6.     }

7.  

8.   
     var transaction = db.transaction(\[\"customers\"\], \"readwrite\");

9.  

10.    // Do something when all the data is added to the database.

11.    transaction.oncomplete = function(event) {

12.      console.log(\"All done!\");

13.    };

14. 

15.    transaction.onerror = function(event) {

16.      console.log(\"transaction.onerror
    errcode=\" + event.target.error.name);

17.    };

18. 

19.    var objectStore = transaction.objectStore(\"customers\");

20. 

21.    var customerToUpdate={};

22.    customerToUpdate.ssn = document.querySelector(\"#ssn\").value;

23.    customerToUpdate.name = document.querySelector(\"#name\").value;

24.    customerToUpdate.age = document.querySelector(\"#age\").value;

25.  
     customerToUpdate.email = document.querySelector(\"#email\").value;

26.  

27.    alert(\'updating customer ssn=\' + customerToUpdate.ssn);

28.    **var request = objectStore.put(customerToUpdate);**

29. 

30.    request.onsuccess = function(event) {

31.      console.log(\"Customer updated.\");

32.    };

33.  

34.    request.onerror = function(event) {

35.      alert(\"request.onerror, could not update customer, errcode=
    \" +

36.         event.target.error.name + \". The ssn is not in the

37.         Database\");

38.   };

39. }

The update occurs at *line 28*.

## 3.6.10 Getting data

There are several ways to retrieve data from a data store.

### First method: getting data when we know its key

The simplest function from the API is the request.get(key) function. It
retrieves an object when we know its key/keypath.

[Online example at JSBin](https://jsbin.com/saquru):

![Getting data from IndexedDB, first enter a ssn, then press the search
button](./images/image045.jpeg){width="6.5in"
height="4.190277777777778in"}

If the ssn exists in the object store, then the results are displayed in
the form itself (the code that gets the results and that updates the
form is in the request.onsuccess callback).

![Form updated with data
retrieved](./images/image046.jpeg){width="6.5in"
height="1.9833333333333334in"}

Here is the code added to that example:

1.  function searchACustomer() {

2.     if(db === null) {

3.       alert(\'Database must be opened first, please click the Create

4.              CustomerDB Database first\');

5.       return;

6.     }

7.  

8.   
     var transaction = db.transaction(\[\"customers\"\], \"readwrite\");

9.  

10.    // Do something when all the data is added to the database.

11.    transaction.oncomplete = function(event) {

12.      console.log(\"All done!\");

13.    };

14. 

15.    transaction.onerror = function(event) {

16.      console.log(\"transaction.onerror
    errcode=\" + event.target.error.name);

17.    };

18. 

19.    var objectStore = transaction.objectStore(\"customers\");

20. 

21.    // Init a customer object with just the ssn property initialized

22.    // from the form

23.    **var customerToSearch={};**

24.  
     **customerToSearch.ssn = document.querySelector(\"#ssn\").value;**

25. 

26.    alert(\'Looking for customer ssn=\' + customerToSearch.ssn);

27. 

28.    // Look for the customer corresponding to the ssn in the object

29.    // store

30.    **var request = objectStore.get(customerToSearch.ssn);**

31. 

32.    request.onsuccess = function(event) {

33.      **console.log(\"Customer found\" + event.target.result.name);**

34.    
     document.querySelector(\"#name\").value=event.target.result.name;

35.    
     document.querySelector(\"#age\").value = event.target.result.age;

36.      document.querySelector(\"#email\").value

37.                                         =event.target.result.email;

38.    };

39.  

40.    request.onerror = function(event) {

41.      alert(\"request.onerror, could not find customer, errcode =
    \" +              event.target.error.name + \".

42.             The ssn is not in the Database\");

43.   };

44. }

The search is inititated at *line 30*, and the callback in the case of
success is request.onsuccess, *lines 32-38*. event.target with result as
the retrieved object (*lines 33 to 36*).

Well, this is a lot of code, isn\'t it? We can considerably abbreviate
this function (though, admittedly it won\'t take care of all possible
errors). Here is the shortened version:

1.  function searchACustomerShort() {

2.    db.transaction(\"customers\").objectStore(\"customers\")

3.  .get(document.querySelector(\"#ssn\").value).onsuccess =   

4.     function(event) {

5.        document.querySelector(\"#name\").value =

6.                                            event.target.result.name;

7.        document.querySelector(\"#age\").value =

8.                                            event.target.result.age;

9.        document.querySelector(\"#email\").value =

10.                                           event.target.result.email;

11.   }; // end of onsuccess callback

12. }

You can try it on JSBin: this [version of the online example using this
shortened version](https://jsbin.com/rifate) (the function is at the end
of the JavaScript code):

1.  function searchACustomerShort() {

2.     if(db === null) {

3.        alert(\'Database must be opened first, please click the Create

4.               CustomerDB Database first\');

5.        return;

6.     }

7.  

8.     db.transaction(\"customers\").objectStore(\"customers\")

9.       .get(document.querySelector(\"#ssn\").value)

10.      .onsuccess = 

11.        function(event) {

12.           document.querySelector(\"#name\").value =

13.                                      event.target.result.name;

14.           document.querySelector(\"#age\").value =

15.                                      event.target.result.age;

16.           document.querySelector(\"#email\").value =

17.                                      event.target.result.email;

18.        };

19. }

### **Explanations:**

-   Since there\'s only one object store, you can avoid passing a list
    of object stores that you need in your transaction and just pass the
    name as a string (*line 8*),

-   We are only reading from the database, so we don\'t need a
    \"readwrite\" transaction. Calling transaction() with no mode
    specified gives a \"readonly\" transaction (*line 8*),

-   We don\'t actually save the request object to a variable. Since the
    DOM event has the request as its target we can use the event to get
    to the result property (*line 9*).

### Second method: getting more than one piece of data

Getting all of the data from the datastore: using a cursor.

Using get() requires that you know which key you want to retrieve. If
you want to step through all the values in your object store, or just
between those in a certain range, then you must use *a cursor*.

### Here\'s what it looks like:

1.  function listAllCustomers() {

2.     var objectStore =   

3.       db.transaction(\"customers\").objectStore(\"customers\");

4.  

5.     **objectStore.openCursor().onsuccess **= function(event) {

6.       // we enter this callback for each object in the store

7.  

8.       **// The result is the cursor itself**

9.       **var cursor = event.target.result;**

10. 

11.      if (cursor) {

12.        alert(\"Name for SSN \" +** cursor.key **+ \" is \" +

13.               **cursor.value.name**);

14.        // Calling continue on the cursor will result in this
    callback

15.        // being called again if there are other objects in the store

16.        **cursor.continue();**

17.      } else {

18.        alert(\"No more entries!\");

19.      }

20.   }; // end of onsuccess\...

21. } // end of listAllCustomers()

[You can try this example on JSBin](https://jsbin.com/xetumu).

It adds a button to our application. Clicking on it will display a set
of alerts, each showing details of an object in the object store:

![Screenshot with a \"list all customers button\" and an alert showing
one of them](./images/image047.jpeg){width="5.0in"
height="1.4529910323709536in"}

The openCursor() function can take several (optional) arguments.

-   First, you can limit the range of items that are retrieved by using
    a key range object - we\'ll get to that in a minute.

-   Second, you can specify the direction that you want to iterate.

In the above example, we\'re iterating over all objects in ascending
order. The onsuccess callback for cursors is a little special. **The
cursor object itself is the result property of the request** (above
we\'re using the shorthand, so it\'s event.target.result). Then **the
actual key and value can be found on the key and value properties of the
cursor object**. If you want to keep going, then you have to
call cursor.continue() on the cursor.

When you\'ve reached the end of the data (or if there were no entries
that matched your openCursor() request) you still get
a success callback, but the result property is undefined.

One common pattern with cursors is to retrieve all objects in an object
store and add them to an array, like this:

1.  function listAllCustomersArray() {

2.    var objectStore =   

3.        db.transaction(\"customers\").objectStore(\"customers\");

4.  

5.    var customers = \[\]; // the array of customers that will hold

6.                        // results

7.  

8.    objectStore.openCursor().onsuccess = function(event) {

9.      var cursor = event.target.result;

10. 

11.     if (cursor) {

12.       customers.push(cursor.value); // add a customer in the

13.                                     // array

14.       cursor.continue();

15.     } else {

16.       alert(\"Got all customers: \" + customers);

17.     }

18.  }; // end of onsuccess

19. } // end of listAllCustomersArray()

[You can try this version on JSBin](https://jsbin.com/bitoqa).

### Getting data using an index

Storing customer data using the ssn as a key is logical since
the ssn uniquely identifies an individual. If you need to look up a
customer by name, however, you\'ll need to iterate over every ssn in the
database until you find the right one.

Searching in this fashion would be very slow. Instead, we use *an
index*.

Remember that we defined two indexes in our data store:

1.  one on the name (non-unique) and

2.  one on the email properties (unique).

Here is a function that examines by name the person-objects in the
object store, and returns the first one it finds with a name equal to
\"Bill\":

1.  function getCustomerByName() {

2.     if(db === null) {

3.       alert(\'Database must be opened first, please click the Create

4.              CustomerDB Database first\');

5.       return;

6.     }

7.  

8.     var objectStore =   

9.        db.transaction(\"customers\").objectStore(\"customers\");

10. 

11.    **var index = objectStore.index(\"name\");**

12. 

13.    **index.get(\"Bill\").onsuccess **= function(event) {

14.       alert(\"Bill\'s SSN is \" + **event.target.result.ssn **+

15.             \" his email is \" + **event.target.result.email**);

16.    };

17. }

The search by index occurs at *lines 11 and 13*: *line 11* creates an
\"index\" object that corresponds to the \"name\" property. *Line
13* calls the get() method on this index-object to retrieve all of
the person-objects from the dataStore which have a name equal to
\"Bill\".

[Online example you can try at JsBin](https://jsbin.com/gituxa)

![retrieving data using an index. The screenshot shows a button \"look
for all customers named Bill\", and shows an alert with the
result.](./images/image048.jpeg){width="5.0in"
height="3.9433759842519684in"}

The above example retrieves only the first object that has a name/index
with the value=\"Bill\". Notice that there are two \"Bill\"s in the
object store.

### **Retrieving more than one result when using an index**

In order to get all the \"Bills\", once again we have to use *a cursor*.

When we work with indexes, we can open two different types of cursors on
indexes:

1.  **A normal cursor** which maps the index property to the object in
    the object store, or,

2.  **A key cursor** which maps the index property to the key used to
    store the object in the object store.

### The differences are illustrated below.

### Normal cursor:

1.  index.openCursor().onsuccess = function(event) {

2.  var cursor = event.target.result;

3.  if (cursor) {

4.  // cursor.key is a name, like \"Bill\", and **cursor.value is the**

5.  // **whole object.**

6.  alert(\"Name: \" + cursor.key + \", SSN: \" + cursor.value.ssn + \",

7.  email: \" + cursor.value.email);

8.  **cursor**.continue();

9.  }

10. };

### Key cursor:

1.  index.openKeyCursor().onsuccess = function(event) {

2.     var cursor = event.target.result;

3.     if (cursor) {

4.       // cursor.key is a name, like \"Bill\",** and cursor.value is
    the**

5.  **     **//** SSN (the key)**.

6.       // No way to directly get the rest of the stored object.

7.       alert(\"Name: \" + cursor.key + \", \"SSN: \"
    + **cursor.value**);

8.       cursor.continue();

9.     }

10. };

### Can you see the difference? 

You can try [an online example at JSBin that uses the above
methods](https://jsbin.com/kubuwof):

![getting data using index. The screenshot shows two buttons: one for
getting one single data and one for getting all data, using
indexes](./images/image049.jpeg){width="5.0in"
height="3.427884951881015in"}

### How to try this example:

1.  Press the create/Open CustomerDB database,

2.  Add some more customers,

3.  Then press the last button \"look for all customers with name=Bill
    \...\". This will iterate over all the customers in the object store
    whose name is equal to \"Bill\". There should be two \"Bills\", if
    this is not the case, add two customers with a name equal to
    \"Bill\", then press the last button again.

### Source code extract from this example:

1.  function getAllCustomersByName() {

2.    if(db === null) {

3.      alert(\'Database must be opened first, please click the Create

4.             CustomerDB Database first\');

5.      return;

6.    }

7.  

8.    var objectStore =

9.       db.transaction(\"customers\").objectStore(\"customers\");

10. 

11.   var index = objectStore.index(\"name\");

12. 

13.   // Only match \"Bill\"

14.   var singleKeyRange = IDBKeyRange.only(\"Bill\");

15. 

16.   **index**.openCursor(singleKeyRange).onsuccess = function(event) {

17. 

18.     var cursor = event.target.result;

19. 

20.     if (cursor) {

21.       // cursor.key is a name, like \"Bill\", and cursor.value is
    the

22.       // whole object.

23.       alert(\"Name: \" + cursor.key + \", SSN:
    \" + cursor.value.ssn \",

24.              + email: \" + cursor.value.email);

25.       cursor.continue();

26.    }

27. };

28. }

## 3.6.11 Limiting the range of values in a cursor

How to specify the range and direction of cursors with IndexedDB?

It is possible to use a special object called IDBKeyRange, for
\"IndexedDB Key Range\", and pass it as the first argument
to openCursor() or openKeyCursor().

We can specify the bounds of the data we are looking for, by using
methods such as upperBound() or lowerBound(). The bound may be
\"closed\" (i.e., the key range includes the given value(s)) or \"open\"
(i.e., the key range does not include the given value(s)). 

Let\'s look at some examples ([adapted from this MDN
article](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API/Using_IndexedDB#Specifying_the_range_and_direction_of_cursors)):

1.  // Only match \"Donna\"

2.  var singleKeyRange = IDBKeyRange.only(\"Donna\");

3.   

4.  // Match anything past \"Bill\", including \"Bill\"

5.  var lowerBoundKeyRange = IDBKeyRange.lowerBound(\"Bill\");

6.   

7.  // Match anything past \"Bill\", but don\'t include \"Bill\"

8.  var lowerBoundOpenKeyRange = IDBKeyRange.lowerBound(\"Bill\", true);

9.   

10. // Match anything up to, but not including, \"Donna\"

11. var upperBoundOpenKeyRange = IDBKeyRange.upperBound(\"Donna\", true);

12.  

13. // Match anything between \"Bill\" and \"Donna\", but not including
    \"Donna\"

14. var boundKeyRange = IDBKeyRange.bound(\"Bill\", \"Donna\", false, true);

15.  

16. // To use one of the key ranges, pass it in as the first argument of
    openCursor()/openKeyCursor()

17. index.openCursor(boundKeyRange).onsuccess = function(event) {

18.     var cursor = event.target.result;

19.     if (cursor) {

20.         // Do something with the matches.

21.         cursor.continue();

22.     }

23. };

### Complete example

Adapted from an example on gitHub, today no more available ([original
URL](https://github.com/mdn/IDBKeyRange-example/blob/gh-pages/index.html)):

Try [the online example at JsBin](https://jsbin.com/lawaju/edit) (enter
\"Gaming\", \"Batman\" etc. as key range values):

![Example of use of
IdbKeyRange](./images/image050.jpeg){width="5.0in"
height="5.029379921259842in"}

![IDBKeyRange in
action](./images/image051.jpeg){width="5.0in"
height="4.612179571303587in"}

## 3.6.12 Discussion and projects

Here is the discussion forum for this part of the course. Please post
your comments/observations/questions and share your creations.

### Suggested topics of discussion:

-   IndexedDB is certainly the most complex API presented in this
    course. However, using it is rather simple once you\'ve climbed the
    learning curve. If you have prior experience with databases, can you
    tell your feelings in the forum?

-   If you found handy tools for using IndexedDB, or other external
    tutorials and examples, please share!

### Optional projects:

-   Start from the examples provided in the IndexedDB course and adapt
    them in order to manage a database of the HTML5 interactive examples
    (also provided in this course). For example, objects stores in the
    datastore may be composed of:

-   the jsbin.com URL of the example,

-   a description,

-   the name of the week in which the example has been presented, and,

-   the name of the lesson in the chapter,

-   eventually, a screenshot for the example (URL, or if you are a bit
    > of a geek, image content).

-   Produce an HTML page which contains your application. When loaded,
    it must populate the indexedDB database with at least 10 different
    examples, and display them in a table or in a list. The GUI must
    also provide a search form for retrieving all the examples from a
    given chapter. 

## Conclusion

The two W3Cx courses, [HTML5 Coding Essentials and Best
Practices](https://www.edx.org/course/html5-coding-essentials-and-best-practices) and
this one (HTML5 Apps and Games), have covered a lot of material, and you
may have trouble identifying which of the different techniques you have
learned best suit your needs.

### To sum up:

-   **If you need to work with transactions** (in the database sense:
    protect data against concurrent access, etc.), or do some searches
    on a large amount of data, if you need indexes, etc., **then use
    IndexedDB**

-   **If you need a way to store simple strings or JSON objects, then
    use localStorage/sessionStorage**. *Example*: store HTML form
    content as you type, store a game\'s hi-scores, preferences of an
    application, etc.

-   **If you need to manipulate files (read or download/upload), then
    use the File API and XHR2.**

-   If you need to manipulate a file system, there is a FileSystem and a
    FileWriter API which are very poorly supported and will certainly be
    replaced in HTML 5.1. We decided not to discuss these in the course
    because they lack agreement within the community and browser
    vendors.

-   If you need an SQL database client-side: No! Forget this idea,
    please! There was once a WebSQL API, but it disappeared rapidly.

> **Note that the above points may be used in any combination**: you may
> have a Web app that uses localStorage and IndexedDB to cache its
> resources so that it can run in offline mode.

### External resources

-   You might be interested by [the Cache
    API](https://developers.google.com/web/fundamentals/instant-and-offline/web-storage/cache-api) to
    make your application data available offline (in other terms: making
    your Web page or your Web app. available offline). 

-   Read also [this article that covers all different options for
    storing data in the browser and gives another look at what has been
    presented in this chapter of the
    course](https://web.dev/storage-for-the-web/).

