---
layout: content
menu: learn
title: Getting Started
---

# Getting Started

This chapter will guide you through setup and some basic examples to get you going.  For advance API coverage please refer to each topic within the overall guide.

## Setting Up Your Environment

### Maven Configuration

{% capture md %}
{% include maven.md %}
{% endcapture %}
{{ md | markdownify }}

### Non-Maven Users

If you do not use Maven you can download from one of the links below and add the library to your class path.

<table class="table table-striped">
  <tr><th><strong>Version</strong></th><th><strong>Type</strong></th><th><strong>Link</strong></th></tr>
  <tr><td>{{ site.version }}</td><td>Stable/Release</td><td><a class="btn btn-success btn-small" href="/downloads/openstack4j-{{ site.version }}.jar" target="_blank">Download</a></td></tr>
  <tr><td>{{ site.snapshot-version }}</td><td>Development</td><td><a class="btn btn-warning btn-small" href="/downloads/openstack4j-{{ site.snapshot-version }}.jar" target="_blank">Download</a></td></tr>
</table>
<br>

## Lets Play!

Let's test your OpenStack deployment with the API.  For advance coverage of the API please refer to the service of interest on the left navigation pane.
<br><br>

### Authenticate

Creating and authenticating against OpenStack is extremely simple. Below is an example of authenticating which will result with the authorized OSClient. OSClient allows you to invoke Compute, Identity, Neutron operations fluently.

In the example below we are specifying the OpenStack deployment endpoint to connect to, user credentials to authenticate and the default tenant we would like to be in context of.
<br>

{:.prettyprint .lang-java}
	OSClient os = OSFactory.builder()
	                       .endpoint("http://127.0.0.1:5000/v2.0")
	                       .credentials("admin","sample")
	                       .tenantName("admin")
	                       .authenticate();
						

### Run some Queries

Now that we have successfully authenticated and have a client we will show you a few basic examples of grabbing data from the various services.  These are high level and for full CRUD and management calls please refer to each individual service guide.

{:.prettyprint .lang-java}
	// Find all Users
	List<User> users = os.identity().users().list();
	
	// List all Tenants
	List<Tenant> tenants = os.identity().tenants().list();
	
	// Find all Compute Flavors
	List<Flavor> flavors = os.compute().flavors().list();
	
	// Find all running Servers
	List<Server> servers = os.compute().servers().list();
	
	// Suspend a Server
	os.compute().servers().action("serverId", Action.SUSPEND);
	
	// List all Networks
	List<Network> networks = os.networking().network().list();
	
	// List all Subnets
	List<Subnet> subnets = os.networking().subnet().list();
	
	// List all Routers
	List<Router> routers = os.networking().router().list();
	
	// List all Images (Glance)
	List<Image> images = os.images().list();
	
	// Download the Image Data
	InputStream is = os.images().getAsStream("imageId");

As you can see in the examples above we have exercised a small portion of the following services (Identity, Computer, Network and Image).