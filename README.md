

Camel Route -->

        <route id="transformjsontoxml">
            <from id="_from3" uri="direct:transformjsontoxml"/>
            <log id="_log11" message="In Route Block for ROUTE ${routeId} "/>
            <log id="_log21" message="The In  Body is ${body}"/>
            <to id="_to11" uri="atlas:classpath:atlasmap-mapping-customtrans.adm"/>
            <log id="_log31" message="The Out Body is ${body}"/>
        </route>


Error:


18:44:54.444 [XNIO-1 task-1] INFO  transformjsontoxml - The In  Body is {
  "order": {
    "address": {
      "city": "Westford",
      "state": "test",
      "street": "1040 Notexisting St",
      "zip": "01886"
    },
    "contact": {
      "firstName": "Bob",
      "lastName": "Totton",
      "phone": "12-4567890"
    },
    "orderId": "O001"
  }
}
18:44:54.553 [XNIO-1 task-1] WARN  io.atlasmap.core.ADMArchiveHandler - Invalid serialized mapping definition content detected, discarding
18:44:54.554 [XNIO-1 task-1] WARN  io.atlasmap.core.DefaultAtlasContext - AtlasMap context cannot initialize without mapping definition, ignoring: Mapping URI=null
18:44:54.557 [XNIO-1 task-1] INFO  transformjsontoxml - In Exception Block and Exception is  for ROUTE transformjsontoxml
18:44:54.561 [XNIO-1 task-1] ERROR o.a.c.processor.DefaultErrorHandler - Failed delivery for (MessageId: ID-MacBook-Pro-1636982086742-0-2 on ExchangeId: ID-MacBook-Pro-1636982086742-0-1). Exhausted after delivery attempt: 1 caught: java.lang.NullPointerException. Processed by failure processor: FatalFallbackErrorHandler[Channel[Log(transformjsontoxml)[In Exception Block and Exception is ${exception.message} for ROUTE ${routeId}]]]

Message History
---------------------------------------------------------------------------------------------------------------------------------------
RouteId              ProcessorId          Processor                                                                        Elapsed (ms)
[transformData     ] [transformData     ] [servlet:/test/trasnformdata?httpMethodRestrict=POST                           ] [       126]
[transformData     ] [to3               ] [direct:validateandtrasnformdata                                               ] [         0]
[_route1           ] [_choice1          ] [when[simple{${header.Content-Type} == 'application/xml'}]choice[when[simple{${] [         0]
[_route1           ] [_log5             ] [log                                                                           ] [         0]
[_route1           ] [_to3              ] [direct:transformjsontoxml                                                     ] [         0]
[transformjsontoxml] [_log11            ] [log                                                                           ] [         1]
[transformjsontoxml] [_log21            ] [log                                                                           ] [         0]
[transformjsontoxml] [_to11             ] [atlas:classpath:atlasmap-mapping-customtrans.adm                              ] [       113]
[transformjsontoxml] [log9              ] [log                                                                           ] [         0]

Stacktrace
---------------------------------------------------------------------------------------------------------------------------------------
java.lang.NullPointerException: null
	at org.apache.camel.component.atlasmap.AtlasEndpoint.populateSourceDocuments(AtlasEndpoint.java:256)
	at org.apache.camel.component.atlasmap.AtlasEndpoint.onExchange(AtlasEndpoint.java:196)
	at org.apache.camel.impl.ProcessorEndpoint$1.process(ProcessorEndpoint.java:71)
	at org.apache.camel.util.AsyncProcessorConverterHelper$ProcessorToAsyncProcessorBridge.process(AsyncProcessorConverterHelper.java:61)
	at org.apache.camel.processor.SendProcessor.process(SendProcessor.java:148)
	at org.apache.camel.processor.RedeliveryErrorHandler.process(RedeliveryErrorHandler.java:548)
	at org.apache.camel.processor.CamelInternalProcessor.process(CamelInternalProcessor.java:201)
	at org.apache.camel.processor.Pipeline.process(Pipeline.java:138)
	at org.apache.camel.processor.Pipeline.process(Pipeline.java:101)
	at org.apache.camel.processor.CamelInternalProcessor.process(CamelInternalProcessor.java:201)
	at org.apache.camel.component.direct.DirectProducer.process(DirectProducer.java:76)
	at org.apache.camel.processor.SendProcessor.process(SendProcessor.java:148)
	at org.apache.camel.processor.RedeliveryErrorHandler.process(RedeliveryErrorHandler.java:548)
	at org.apache.camel.processor.CamelInternalProcessor.process(CamelInternalProcessor.java:201)
	at org.apache.camel.processor.Pipeline.process(Pipeline.java:138)
	at org.apache.camel.processor.Pipeline.process(Pipeline.java:101)
	at org.apache.camel.processor.ChoiceProcessor.process(ChoiceProcessor.java:117)
	at org.apache.camel.processor.RedeliveryErrorHandler.process(RedeliveryErrorHandler.java:548)
	at org.apache.camel.processor.CamelInternalProcessor.process(CamelInternalProcessor.java:201)
	at org.apache.camel.processor.CamelInternalProcessor.process(CamelInternalProcessor.java:201)
	at org.apache.camel.component.direct.DirectProducer.process(DirectProducer.java:76)
	at org.apache.camel.processor.SendProcessor.process(SendProcessor.java:148)
	at org.apache.camel.processor.RedeliveryErrorHandler.process(RedeliveryErrorHandler.java:548)
	at org.apache.camel.processor.CamelInternalProcessor.process(CamelInternalProcessor.java:201)
	at org.apache.camel.processor.CamelInternalProcessor.process(CamelInternalProcessor.java:201)
	at org.apache.camel.processor.DelegateAsyncProcessor.process(DelegateAsyncProcessor.java:97)
	at org.apache.camel.http.common.CamelServlet.doService(CamelServlet.java:213)
	at org.apache.camel.http.common.CamelServlet.service(CamelServlet.java:79)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:750)
	at io.undertow.servlet.handlers.ServletHandler.handleRequest(ServletHandler.java:74)
	at io.undertow.servlet.handlers.FilterHandler$FilterChainImpl.doFilter(FilterHandler.java:129)
	at org.springframework.web.filter.RequestContextFilter.doFilterInternal(RequestContextFilter.java:100)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:119)
	at io.undertow.servlet.core.ManagedFilter.doFilter(ManagedFilter.java:61)
	at io.undertow.servlet.handlers.FilterHandler$FilterChainImpl.doFilter(FilterHandler.java:131)
	at org.springframework.web.filter.FormContentFilter.doFilterInternal(FormContentFilter.java:93)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:119)
	at io.undertow.servlet.core.ManagedFilter.doFilter(ManagedFilter.java:61)
	at io.undertow.servlet.handlers.FilterHandler$FilterChainImpl.doFilter(FilterHandler.java:131)
	at org.springframework.boot.actuate.metrics.web.servlet.WebMvcMetricsFilter.doFilterInternal(WebMvcMetricsFilter.java:93)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:119)
	at io.undertow.servlet.core.ManagedFilter.doFilter(ManagedFilter.java:61)
	at io.undertow.servlet.handlers.FilterHandler$FilterChainImpl.doFilter(FilterHandler.java:131)
	at org.springframework.web.filter.CharacterEncodingFilter.doFilterInternal(CharacterEncodingFilter.java:201)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:119)
	at io.undertow.servlet.core.ManagedFilter.doFilter(ManagedFilter.java:61)
	at io.undertow.servlet.handlers.FilterHandler$FilterChainImpl.doFilter(FilterHandler.java:131)
	at io.undertow.servlet.handlers.FilterHandler.handleRequest(FilterHandler.java:84)
	at io.undertow.servlet.handlers.security.ServletSecurityRoleHandler.handleRequest(ServletSecurityRoleHandler.java:62)
	at io.undertow.servlet.handlers.ServletChain$1.handleRequest(ServletChain.java:68)
	at io.undertow.servlet.handlers.ServletDispatchingHandler.handleRequest(ServletDispatchingHandler.java:36)
	at io.undertow.servlet.handlers.RedirectDirHandler.handleRequest(RedirectDirHandler.java:68)
	at io.undertow.servlet.handlers.security.SSLInformationAssociationHandler.handleRequest(SSLInformationAssociationHandler.java:117)
	at io.undertow.servlet.handlers.security.ServletAuthenticationCallHandler.handleRequest(ServletAuthenticationCallHandler.java:57)
	at io.undertow.server.handlers.PredicateHandler.handleRequest(PredicateHandler.java:43)
	at io.undertow.security.handlers.AbstractConfidentialityHandler.handleRequest(AbstractConfidentialityHandler.java:46)
	at io.undertow.servlet.handlers.security.ServletConfidentialityConstraintHandler.handleRequest(ServletConfidentialityConstraintHandler.java:64)
	at io.undertow.security.handlers.AuthenticationMechanismsHandler.handleRequest(AuthenticationMechanismsHandler.java:60)
	at io.undertow.servlet.handlers.security.CachedAuthenticatedSessionHandler.handleRequest(CachedAuthenticatedSessionHandler.java:77)
	at io.undertow.security.handlers.AbstractSecurityContextAssociationHandler.handleRequest(AbstractSecurityContextAssociationHandler.java:43)
	at io.undertow.server.handlers.PredicateHandler.handleRequest(PredicateHandler.java:43)
	at io.undertow.servlet.handlers.SendErrorPageHandler.handleRequest(SendErrorPageHandler.java:52)
	at io.undertow.server.handlers.PredicateHandler.handleRequest(PredicateHandler.java:43)
	at io.undertow.servlet.handlers.ServletInitialHandler.handleFirstRequest(ServletInitialHandler.java:269)
	at io.undertow.servlet.handlers.ServletInitialHandler.access$100(ServletInitialHandler.java:78)
	at io.undertow.servlet.handlers.ServletInitialHandler$2.call(ServletInitialHandler.java:133)
	at io.undertow.servlet.handlers.ServletInitialHandler$2.call(ServletInitialHandler.java:130)
	at io.undertow.servlet.core.ServletRequestContextThreadSetupAction$1.call(ServletRequestContextThreadSetupAction.java:48)
	at io.undertow.servlet.core.ContextClassLoaderSetupAction$1.call(ContextClassLoaderSetupAction.java:43)
	at io.undertow.servlet.handlers.ServletInitialHandler.dispatchRequest(ServletInitialHandler.java:249)
	at io.undertow.servlet.handlers.ServletInitialHandler.access$000(ServletInitialHandler.java:78)
	at io.undertow.servlet.handlers.ServletInitialHandler$1.handleRequest(ServletInitialHandler.java:99)
	at io.undertow.server.Connectors.executeRootHandler(Connectors.java:387)
	at io.undertow.server.HttpServerExchange$1.run(HttpServerExchange.java:841)
	at org.jboss.threads.ContextClassLoaderSavingRunnable.run(ContextClassLoaderSavingRunnable.java:35)
	at org.jboss.threads.EnhancedQueueExecutor.safeRun(EnhancedQueueExecutor.java:2019)
	at org.jboss.threads.EnhancedQueueExecutor$ThreadBody.doRunTask(EnhancedQueueExecutor.java:1558)
	at org.jboss.threads.EnhancedQueueExecutor$ThreadBody.run(EnhancedQueueExecutor.java:1423)
	at org.xnio.XnioWorker$WorkerThreadFactory$1$1.run(XnioWorker.java:1280)
	at java.lang.Thread.run(Thread.java:748)

