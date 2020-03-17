# Cloud Native Spatial with PostGIS
## Getting pg_featureserv and pg_tileserv up and running on Kubernetes

You probably already read about [pg_featureserv]() and [pg_tileserv]() along with their intended place in the [spatial ecosystem]()  (if you haven’t, go read those links now - we’ll wait for you). You have also heard about containers and Kubernetes - you may even be evaluating or running it. Well today’s piece is going to show you how simple and easy it is to run these new spatial servers alongside PostGIS in your cloud native architecture. Along the way we will point out some of the ways in which these projects fit so nicely into your cloud native or microservices architecture.


## Assumptions/Prerequisites

Before we get started I assume you already 
1. Have a Kuberentes or OpenShift cluster up and running. It should be greater than Kubernetes 1.13 and OpenShift 3.11. 
1. You should also have the Crunchy Postgres Operator (hereafter referred to as *operator*) installed in your Kube or OpenShift cluster and ready to deploy a PostGIS cluster. 
1. You have the pgo client utility on your local machine and set up to talk to your cluster
1. We assume you understand [Kubernetes]() and [OpenShift]() concepts, so if you see one here that you don’t understand you will know how to find more information. 
1. We also assume you know how to use PostGIS, especially importing data.

For this blog post we are going to use OpenShift because it has a nicer interface and user experience for working with Kubernetes Objects. We installed the Crunchy Operator in a namespace called **pgo** and we are going to put all our work in a namespace named **blog**. We will create the **blog** namespace with the Crunchy operator.

## Provisioning Your Database

So let’s get started by provisioning our database. The first step is going to be getting `pgo` client tool, used to interact with the Crunchy Operator, talking to the API container in the operator pod

Since we are using OpenShift we are going to use the `oc` command line tool to get our `pgo` connection working. Make sure your `oc` client is authenticated to your cluster and then away we go

```

```







