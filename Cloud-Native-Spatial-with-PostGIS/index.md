# Cloud Native Spatial with PostGIS
## Getting pg_featureserv and pg_tileserv up and running on Kubernetes

You probably already read about [pg_featureserv]() and [pg_tileserv]() along with their intended place in the [spatial ecosystem]()  (if you haven’t, go read those links now - we’ll wait for you). You have also heard about containers and Kubernetes - you may even be evaluating or running it. Well today’s piece is going to show you how simple and easy it is to run these new spatial servers alongside PostGIS in your cloud native architecture. Along the way we will point out some of the ways in which these projects fit so nicely into your cloud native or microservices architecture.

## Assumptions and Prequisites


 ## Let's get spatial!
 
 Now that we have our data loaded into PostGIS it's time to get the spatial app servers into Kubernetes/OpenShift. Given that these pieces were built to be cloud native you will see how easy it is to run them in a cloud platform. After that we'll scale them up with ease.
 
 ### Starting with pg_featureserv
 
 Luckily for us OpenShift has a nice command for adding containers to run in Kubernetes. We can do a simple command and load our container into kubernetes with very reasonable defaults for running. So with that let's get going. Here is the command to load the container from Docker hub or the Crunchy container repo.  TODO  FILL THIS IN WITH BOTH REPOS






