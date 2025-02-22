+++
title = "Set default submit button on a page with GWT"
slug = "2014-02-16-set-default-submit-button-on-a-page-with-gwt"
published = 2014-02-16T00:32:00.002000-08:00
author = "Pandurang Patil"
tags = [ "GWT", "GoogleWebToolkit"]
+++
I found few ways to set default submit button on page with GWT. 

1. Add key press handler for all form fields check for `Enter` button press and take action. You can add common key press handler for all form fields. This way you are not adding multiple handler for each form field. (I am
assuming you understand what is `ui handler` and how it works.)
  
```
@UiHandler({ "txtCompanyName", "txtcontactName", "txtEmail" })
public void onKeyPress(KeyPressEvent event) {
     if (event.getNativeEvent().getKeyCode() == KeyCodes.KEY_ENTER) {
          // TODO: Take your action.
     }
}
```

2. Enclose all your form fields inside `com.google.gwt.user.client.ui.FocusPanel` and handle key press event on this focus panel.

```
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
```

3. Add page wide native event handler and intercept each event, check if it is `Enter` button and take your action.

```
     Event.addNativePreviewHandler(new NativePreviewHandler() {

          @Override
          public void onPreviewNativeEvent(NativePreviewEvent event) {
               if (event.getNativeEvent().getKeyCode() == KeyCodes.KEY_ENTER) {
                    // TODO: Take your action.
               }
          }
     });
```
