+++
title = "GWT use I18 Message resource in uiBinder"
slug = "2012-05-20-gwt-use-i18-message-resource-in-uibinder"
published = 2012-05-20T12:20:00.001000-07:00
author = "Pandurang Patil"
tags = [ "i18", "GWT", "messages", "GoogleWebToolkit", "uibinder",]
+++
To use I18 Message resource in `uiBinder` you need to follow the same mechanism as that of ClientBundle  
  
In your corresponding java class add `@uiFactory` method which will return the object of required Message interface 

e.g. 


    package com.test.module.client;
      
    public interface Messages extends com.google.gwt.i18n.client.Messages
    {
    	@DefaultMessage("Home") 
    	@Key("home")
     	@DefaultMessage("Home")
     	String home();
    }
    
    public class MyUiBinder extends Composite{
    .....  
    .....  
    	@UiFactory
     	public static Messages getResources() {
     		return GWT.create(Messages.class); 
     	}
     }		
    
    


And you can use the same inside corresponding `MyUiBinder.ui.xml` file as  

    <ui:UiBinder xmlns:ui=‘urn:ui:com.google.gwt.uibinder’ xmlns:g=‘urn:import:com.google.gwt.user.client.ui’>
    	<ui:with field=‘msg’ type=‘com.test.module.client.Messages’ />
    	<g:HTMLPanel>
    		<g:Button text=’{msg.home}’></g:Button>
    		……
    		……
    	</g:HTMLPanel>
    </ui:UiBinder>		

