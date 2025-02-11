+++
title = "Intercept GWT RPC Request and Response"
slug = "2013-01-20-intercept-gwt-rpc-request-and-response"
published = 2013-01-20T11:01:00.001000-08:00
author = "Pandurang Patil"
tags = [ "RPC", "GWT", "RequestFactory"]
+++
Some times you want to do some generic things like setting some header
or adding some log or may be even showing a progress bar while rpc call
is in progress and hide it once you receive the response. I came across
one of such requirement for showing progress bar while service call is
in progress. Following is complete end to end solution I found after
searching for some solutions. I got some help at following threads
<https://groups.google.com/forum/?fromgroups=#!msg/google-web-toolkit/VeiJUPBUsi4/Hq2VDMF9W1kJ>
and
<http://stackoverflow.com/questions/5309624/how-to-intercept-the-onsuccess-method-in-gwt>  
  
I created one complete end to end working example from that help.  
  

    1:  public class LoaderRpcRequestBuilder extends RpcRequestBuilder {  
    2:       private Loader     loader;  
    3:       private class RequestCallbackWrapper implements RequestCallback {  
    4:            private RequestCallback     callback;  
    5:            RequestCallbackWrapper(RequestCallback aCallback) {  
    6:                 this.callback = aCallback;  
    7:            }  
    8:            @Override  
    9:            public void onResponseReceived(Request request, Response response) {  
    10:                 loader.hide();  
    11:                 callback.onResponseReceived(request, response);  
    12:            }  
    13:            @Override  
    14:            public void onError(Request request, Throwable exception) {  
    15:                 loader.hide();  
    16:                 callback.onError(request, exception);  
    17:            }  
    18:       }  
    19:       public LoaderRpcRequestBuilder(Loader loader) {  
    20:            this.loader = loader;  
    21:       }  
    22:       public LoaderRpcRequestBuilder() {  
    23:            this(new Loader());  
    24:       }  
    25:       @Override  
    26:       protected RequestBuilder doCreate(String serviceEntryPoint) {  
    27:            RequestBuilder rb = super.doCreate(serviceEntryPoint);  
    28:            loader.show();  
    29:            return rb;  
    30:       }  
    31:       @Override  
    32:       protected void doFinish(RequestBuilder rb) {  
    33:            super.doFinish(rb);  
    34:            rb.setCallback(new RequestCallbackWrapper(rb.getCallback()));  
    35:       }  
    36:  }  

  
Here in above code we are creating our own custom RpcRequestBuilder by
extending RpcRequestBuilder and by overriding its doCreate and
doFinish() method. We are intercepting the calls that will be made. In
doCreate() we are showing loader and then inside doFinish we are setting
one general purpose RequestCallback wrapper which we have created to
intercept response received. Where we are hiding our loader inside
onResponseReceived() and onError.  
  
Note: be sure to call super.doFinish(rb); other wise you will get
SecurityException. There are some tokens which is set by doFinish method
to avoid XSRF attack. (Though they say one should not just rely on this
mechanism to avoid XSRF attack.)  
  
Now that we have created custom RpcRequestBuilder we need to understand
how to use it.  
  

    1:  ServiceAsync serivce = GWT.create(Service.class);  
    2:  ServiceDefTarget target = (ServiceDefTarget) serivce;  
    3:  target.setRpcRequestBuilder(new LoaderRpcRequestBuilder());  

  
When we make rpc call we get async instance before making any service
call we need to set our own custom RpcRequestBuilder.
