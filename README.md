# swarm-jaxrs-static-problem

This project demonstrates a problem with using resteasy html provider together with wildfly swarm to build a simple static web application

In a current state (commented out resteasy-html dependency) jaxrs endpoint works, but neither of static resources are working

If we uncomment resteasy-html dependency and rebuild app, jaxrs endpoint does not work anymore - either pure jaxrs or resteasy html view (see HelloWorldEndpoint.java.bak).

Instead, static files start working, but not completely - favicon.ico is still replaced by fallback one. 

I think this is clearly some kind of classloading problem, but also a conflict between resteasy and undertow. 

I found a number of issues dedicated to the conflict between jaxrs and undertow, which recommend to use ApplicationPath annotation to move jaxrs from root, 
but this is not acceptable with my resteasy-html resources - I need them to be root resources. 

Other solution, with deploying resteasy as a filter, also did not work for me, again likely due to the classloading issues. 
