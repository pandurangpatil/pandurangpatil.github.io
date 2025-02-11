+++
title = "Set default submit button on a page with GWT"
slug = "2014-02-16-set-default-submit-button-on-a-page-with-gwt"
published = 2014-02-16T00:32:00.002000-08:00
author = "Pandurang Patil"
tags = [ "GWT", "GoogleWebToolkit"]
+++
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">I
found few ways to set default submit button on page with GWT. </span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">1.
Add key press handler for all form fields check for enter button and
take action. You can add common key press handler for all form fields.
This way you are not adding multiple handler for each form field. (I am
assuming you understand what is ui handler and how it works.)</span>  
  

     @UiHandler({ "txtCompanyName", "txtcontactName", "txtEmail" })
     public void onKeyPress(KeyPressEvent event) {
      if (event.getNativeEvent().getKeyCode() == KeyCodes.KEY_ENTER) {
       // TODO: Take your action.
      }
     }

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span><span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">2.
 Enclose all your form fields
inside com.google.gwt.user.client.ui.FocusPanel and handle key press
event on this focus panel.</span>  

     @UiField
     FocusPanel mainPanel;
            .
            .
            .
     @UiHandler("mainPanel")
     public void allkyePressHandler(KeyPressEvent event) {
      if (event.getNativeEvent().getKeyCode() == KeyCodes.KEY_ENTER) {
       // TODO: Take your action.
      }
     }

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span><span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">3.
Add page wide native event handler and intercept each event, check if it
is enter button and take your action.</span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span>  

     Event.addNativePreviewHandler(new NativePreviewHandler() {

      @Override
      public void onPreviewNativeEvent(NativePreviewEvent event) {
       if (event.getNativeEvent().getKeyCode() == KeyCodes.KEY_ENTER) {
        // TODO: Take your action.
       }
      }
     });

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span>
