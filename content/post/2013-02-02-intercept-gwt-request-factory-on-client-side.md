+++
title = "Intercept GWT Request Factory on client side"
slug = "2013-02-02-intercept-gwt-request-factory-on-client-side"
published = 2013-02-02T22:36:00-08:00
author = "Pandurang Patil"
tags = [ "RPC", "GWT", "RequestFactory"]
+++
**How to intercept GWT Request Factory on client before call is being made and
after response is received?**  

One can extend `DefaultRequestTransport` and intercept send call, at the same time writing a wrapper over `TrasnportReceiver` one can intercept response's. Following is the example.
  

    public class LoaderRequestTransport extends DefaultRequestTransport {  
        private Loader     loader;  
        
        public LoaderRequestTransport(Loader loader) {  
            this.loader = loader;  
        }  
        
        public LoaderRequestTransport() {  
            this(new Loader(LoaderResources.INSTANCE.communicating()));  
        }  
        
        @Override  
        public void send(final String payload, final TransportReceiver receiver) {  
            
            final TransportReceiver proxy = new TransportReceiver() {  

                @Override  
                public void onTransportFailure(final ServerFailure failure) {  
                    loader.hide();  
                    receiver.onTransportFailure(failure);  
                }  
                
                @Override  
                public void onTransportSuccess(final String payload) {  
                    loader.hide();  
                    receiver.onTransportSuccess(payload);  
                }  
            };  
            
            loader.show();  
            super.send(payload, proxy);  
        }  
    }  

  
Use this `LoaderRequestTransport`
  

    MVPRequestFactory requestFactory = GWT.create(MVPRequestFactory.class);  
    requestFactory.initialize(eventBus, new LoaderRequestTransport());
