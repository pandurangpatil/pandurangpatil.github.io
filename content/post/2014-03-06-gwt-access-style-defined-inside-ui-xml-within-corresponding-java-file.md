+++
title = "GWT access style defined inside .ui.xml within corresponding .java file"
slug = "2014-03-06-gwt-access-style-defined-inside-ui-xml-within-corresponding-java-file"
published = 2014-03-06T21:28:00.002000-08:00
author = "Pandurang Patil"
tags = ["GWT" , "GoogleWebToolkit", "uiBinder"]
+++
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Some
times you may want to access styles defined inside your Sample.ui.xml
file which you want to access / use from within Sample.java widget
class. You can do that by defining an interface which extends
from com.google.gwt.resources.client.</span><span
style="font-family: 'Helvetica Neue', Arial, Helvetica, sans-serif;">CssResource
and declaring method with name matching exactly that of required style
class name that you have declared inside ui.xml. Refer below
code.</span>  
<span
style="font-family: 'Helvetica Neue', Arial, Helvetica, sans-serif;">  
</span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Sample.ui.xml
contents</span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span>  

    <src path>/com/pandurang/client/ui/Sample.ui.xml

    <ui:UiBinder xmlns:ui='urn:ui:com.google.gwt.uibinder' xmlns:g='urn:import:com.google.gwt.user.client.ui'>
       .
       .
       .
       <ui:style type="com.pandurang.client.ui.Sample.MyStyle">
     .domain {
      margin: 0 auto;
      width: 730px;
     }
      
     .editImg {
      cursor: pointer;
      float: left;
      margin-left: 181px;
     }
       </ui:style>
        <g:HTMLPanel>
            <div>
                <div class="{style.domain}">
                       <!-- Contents.... -->
                </div>
            </div>
        </g:HTMLPanel>
    </ui:UiBinder>

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">You
need to connect &lt;ui:style&gt; tag with corresponding CssResource
interface by using "type" attribute of &lt;ui.style&gt; tag as shown
above.</span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Sample.java
contents</span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span>  

    <src path>/com/pandurang/client/ui/Sample.java

    package com.agnie.useradmin.main.client.ui;

    import com.google.gwt.resources.client.CssResource;
    import com.google.gwt.uibinder.client.UiBinder;
    import com.google.gwt.uibinder.client.UiField;
    import com.google.gwt.user.client.ui.Composite;
    import com.google.gwt.core.client.GWT;

    public class Sample extends Composite {

            interface MyUiBinder extends UiBinder<Widget, Sample> {
     }

     private static MyUiBinder uiBinder = GWT.create(MyUiBinder.class);

     interface MyStyle extends CssResource {
      String domain();
                    String editImg();
     }

     @UiField
     MyStyle      style;

            public Sample(){
                 initWidget(uiBinder.createAndBindUi(this));
            }
    }

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">If
you look at above code, we have defined MyStyle interface and declared
methods with name matching to that of css class names. And instance of
MyStyle will be injected by using @UiField annotation. In your java code
you can make use of style variable to access the styles defined inside
ui.xml.</span>
