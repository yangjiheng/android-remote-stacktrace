<wiki:gadget url="http://stefansundin.com/stuff/flattr/google-project-hosting.xml" border="0" width="66" height="76" up\_uid="2405" up\_title="Android Remote Stacktrace" up\_desc="Remotely log unhandled exceptions in your Android applications" up\_tags="android,development,debugging" up\_url="http://code.google.com/p/android-remote-stacktrace/" />

Remotely log unhandled exceptions in your Android applications.

# Client side usage #

Download the latest trace.jar file found [here](http://code.google.com/p/android-remote-stacktrace/downloads/list). Drop it into your Android project and in the properties for your project add it to "Java Build Path" -> "Libraries".

In your android manifest, you must enable internet access for your application:

```
<uses-permission android:name="android.permission.INTERNET" />
```

In the onCreate method of your activity or in your service, you must call `public static boolean register(Context context)` found in the class `ExceptionHandler`. Do something like this:

```
ExceptionHandler.register(this);
```

# Server side installation #

The default implementation will post the stack trace to http://trace.nullwire.com.

[![](http://trace.nullwire.com/images/remote_logger_screenshot.png)](http://trace.nullwire.com)

If you would like to store your stack traces on your own server, you will have to register the exception handler like this:

```
ExceptionHandler.register(this, "http://your.domain/path"); 
```

At `http://your.domain/path` the client side implementation will expect to find [this simple PHP script](http://code.google.com/p/android-remote-stacktrace/source/browse/server/collect/server.php), which will take three POST parameters: 'package\_name', 'package\_version' and 'stacktrace'.  The collected data is simply stored in a plain text file. You can extend the script to send you an email with the stack trace if you like - just uncomment the last line and change the email address.

# Building the JAR #

The JAR may be built by issuing the following command:

```
ant jar
```

This will produce a `trace.jar` file.

Cleaning up is done by:

```
ant clean
```

# Support #

If you have problems, feel free to drop me a mail at mads.kristiansen@nullwire.com.

# Additional information #

How to integrate stack trace collection with Redmine: http://nullwire.com/capturing_android_exceptions_remotely.

# Contributors #

Thanks to these people, who contributed with code changes and/or bug reports.

[Glen Humphrey](http://glendonhumphrey.com), [Evan Charlton](http://evancharlton.com/), [Peter Hewitt](http://dweebos.com/)

# License #

<tt>
The MIT License<br>
<br>
Copyright (c) 2009 Mads Kristiansen, Nullwire ApS<br>
<br>
Permission is hereby granted, free of charge, to any person obtaining a copy<br>
of this software and associated documentation files (the "Software"), to deal<br>
in the Software without restriction, including without limitation the rights<br>
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell<br>
copies of the Software, and to permit persons to whom the Software is<br>
furnished to do so, subject to the following conditions:<br>
<br>
The above copyright notice and this permission notice shall be included in<br>
all copies or substantial portions of the Software.<br>
<br>
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR<br>
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,<br>
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE<br>
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER<br>
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,<br>
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN<br>
THE SOFTWARE.<br>
</tt>
