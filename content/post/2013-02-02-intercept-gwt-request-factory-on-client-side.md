+++
title = "Intercept GWT Request Factory on client side"
slug = "2013-02-02-intercept-gwt-request-factory-on-client-side"
published = 2013-02-02T22:36:00-08:00
author = "Pandurang Patil"
tags = [ "RPC", "GWT", "RequestFactory"]
+++
**<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">How
to intercept GWT Request Factory on client before call is being made and
after response is received?</span>**  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">One
can extend DefaultRequestTransport and intercept send call, at the same
time writing a wrapper over TrasnportReceiver one can intercept
response's. Following is the example.</span>  
  

    1:  public class LoaderRequestTransport extends DefaultRequestTransport {  
    2:       private Loader     loader;  
    3:       public LoaderRequestTransport(Loader loader) {  
    4:            this.loader = loader;  
    5:       }  
    6:       public LoaderRequestTransport() {  
    7:            this(new Loader(LoaderResources.INSTANCE.communicating()));  
    8:       }  
    9:       @Override  
    10:       public void send(final String payload, final TransportReceiver receiver) {  
    11:            final TransportReceiver proxy = new TransportReceiver() {  
    12:                 @Override  
    13:                 public void onTransportFailure(final ServerFailure failure) {  
    14:                      loader.hide();  
    15:                      receiver.onTransportFailure(failure);  
    16:                 }  
    17:                 @Override  
    18:                 public void onTransportSuccess(final String payload) {  
    19:                      loader.hide();  
    20:                      receiver.onTransportSuccess(payload);  
    21:                 }  
    22:            };  
    23:            loader.show();  
    24:            super.send(payload, proxy);  
    25:       }  
    26:  }  

  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Use
this LoaderRequestTransport</span>  
  

    1:  MVPRequestFactory requestFactory = GWT.create(MVPRequestFactory.class);  
    2:  requestFactory.initialize(eventBus, new LoaderRequestTransport());
