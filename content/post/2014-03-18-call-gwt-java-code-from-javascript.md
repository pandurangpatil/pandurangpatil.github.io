+++
title = "Call GWT Java Code from JavaScript"
slug = "2014-03-18-call-gwt-java-code-from-javascript"
published = 2014-03-18T07:14:00.002000-07:00
author = "Pandurang Patil"
tags = [ "GWT", "GoogleWebToolkit", "JavaScript", "JS"]
+++
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">It is
very easy to call javascript from GWT java code by making use of JSNI.
But calling GWT java code from external java script of JSNI is little
tricky and it becomes more complicate when you have to call instance
method of a GWT java class. For more detail refer GWT official document
([refer](http://www.gwtproject.org/doc/latest/DevGuideCodingBasicsJSNI.html))</span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">**Call
static class method from JavaScript**</span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span><span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">*GWTCode.java*</span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span>  

    package open.pandurang.client.view;

    /**
     * @author Pandurang Patil 18-Mar-2014
     * 
     */
    public class GWTCode {

     public static String hello(String name) {
      return "Hello " + name + "!";
     }

     public static native void exportMethod() /*-{
      $wnd.gwtcode_hello = function(name) {
       return @open.pandurang.client.view.GWTCode::hello(Ljava/lang/String;)(name);
      };
     }-*/;
    }

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">At
line 15 we are exposing this GWTCode.hello method and assign it to
window.gwtcode\_hello. Please note there are two "( )" brackets, first
one will declare parameter types and second will take actual parameters.
Don't worry if you are using eclipse when you press CTRL + SPACE after
method name it will populate corresponding type. Now from java script
code you can call window.gwtcode\_hello("&lt;name&gt;")
method. </span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">NOTE:
If method don't take any argument then line no 15 will look like "return
@open.pandurang.client.view.GWTCode::hello()();"</span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span><span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Entry
Point class </span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
*Sample.java*</span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span>  

    package open.pandurang.client.view;

    import com.google.gwt.core.client.EntryPoint;

    /**
     * Entry point classes define <code>onModuleLoad()</code>.
     */
    public class samples implements EntryPoint {

     public void onModuleLoad() {

      GWTCode.exportMethod();
     }

    }

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span><span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">at
line no 12 you will see we are calling exportMethod to export the
GWTCode Hello method.</span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">html
code</span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">*sample.html*</span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span>  

    <!doctype html>
    <html>
    <head>
    <meta http-equiv="content-type" content="text/html; charset=UTF-8">
    <title>Samples and trials</title>
    <script type="text/javascript" language="javascript" src="sample/sample.nocache.js"></script>
    </head>
    <script type="text/javascript" language="javascript">
     function jsGwtCallTest() {
      var msg = window.gwtcode_hello("Pandurang");
      alert(msg);
     }
    </script>
    </head>
    <body>
        <!-- OPTIONAL: include this if you want history support -->
        <iframe src="javascript:''" id="__gwt_historyFrame" tabIndex='-1' style="position: absolute; width: 0; height: 0; border: 0"></iframe>
        <!-- RECOMMENDED if your web app will not function without JavaScript enabled -->
        <noscript>
            <div
                style="width: 22em; position: absolute; left: 50%; margin-left: -11em; color: red; background-color: white; border: 1px solid red; padding: 4px; font-family: sans-serif">
                Your web browser must have JavaScript enabled in order for this application to display correctly.</div>
        </noscript>
        <button onclick="jsGwtCallTest();">test</button>
    </body>
    </html>

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span><span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">we
are calling this method on event of button click. You will not see any
issues here but if you are calling this method from other .js file on
some events like on page load or something. You need to make sure gwt
entry point has been executed and exported the method.</span>
