+++
title = "Quartz Scheduler with Google Guice"
slug = "2014-04-27-quartz-scheduler-with-google-guice"
published = 2014-04-27T10:37:00.001000-07:00
author = "Pandurang Patil"
tags = [ "Quartz", "Guice",]
+++
To integrate Quartz with Guice. One can follow below steps. The most important part is, we should be able to inject dependencies inside Job.

To provide injectable Scheduler Instance we need to write Scheduler provider as follows:

    import org.quartz.Scheduler;
    import org.quartz.SchedulerException;
    import org.quartz.impl.StdSchedulerFactory;

    import com.google.inject.Inject;
    import com.google.inject.Provider;
    import com.google.inject.Singleton;

    /**
     * @author Pandurang Patil 27-Apr-2014
     * 
     */
    @Singleton
    public class SchedulerProvider implements Provider<Scheduler> {
        private Scheduler scheduler;

        @Inject
        public SchedulerProvider(SchedulerJobFactory jobFactory) throws SchedulerException {
            scheduler = new StdSchedulerFactory().getScheduler();
            scheduler.setJobFactory(jobFactory);
        }

        @Override
        public Scheduler get() {
            return scheduler;
        }
    }

Now that we have defined provider for Scheduler we need to map the same inside Guice Module

    import org.quartz.Scheduler;

    import com.google.inject.AbstractModule;

    /**
     * @author Pandurang Patil 27-Apr-2014
     *
     */
    public class SchedulerModule extends AbstractModule {

        @Override
        protected void configure() {
            bind(Scheduler.class).toProvider(SchedulerProvider.class);
        }

    }

With the above code, we should be able to inject Scheduler instance where we want. Lets look at how we would be able to get dependencies injected inside Job. As instantiation of the Job object is done by Scheduler itself, we just pass on the class name through JobDetails. We need intercept this instantiation process to do that we will write our
own Job Factory as follows:

    import org.quartz.Job;
    import org.quartz.Scheduler;
    import org.quartz.SchedulerException;
    import org.quartz.spi.JobFactory;
    import org.quartz.spi.TriggerFiredBundle;

    import com.google.inject.Inject;
    import com.google.inject.Injector;
    import com.google.inject.Singleton;

    /**
     * @author Pandurang Patil 27-Apr-2014
     * 
     */
    @Singleton
    public class SchedulerJobFactory implements JobFactory {

        @Inject
        private Injector injector;

        @Override
        public Job newJob(TriggerFiredBundle bundle, Scheduler scheduler) throws SchedulerException {
            return (Job) injector.getInstance(bundle.getJobDetail().getJobClass());
        }

    }

We need ask scheduler to use this JobFactory while instantiating Job object. We have already connected scheduler with JobFactory inside SchedulerProvider, look at line number 20 for SchedulerProvider code above

As we are returning same instance from Providers get method. Where ever you will inject Schedular, you will get the same object. Schedule your jobs the way it is done normally there is no change in it.

    import org.quartz.Scheduler;
    import org.quartz.SchedulerException;

    import com.google.inject.Guice;
    import com.google.inject.Inject;
    import com.google.inject.Injector;

    /**
     * @author Pandurang Patil 27-Apr-2014
     * 
     */
    public class SchedulerSample {

        @Inject
        private Scheduler scheduler;

        void start() throws SchedulerException {

            scheduler.start();
        }

        public static void main(String[] args) {
            Injector injector = Guice.createInjector(new SchedulerModule());
            SchedulerSample sample = injector.getInstance(SchedulerSample.class);
            try {
                sample.start();
            } catch (SchedulerException e) {
                System.out.println("Error while starting the scheduler...");
            }
            ...
            ...
        }
    }

