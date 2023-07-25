# Rosa Side meeting

## 1/ Intro, notewell and agenda bashing

## 2/ Content distribution Use cases for Rosa - Luis Contreras

- Interest by ISPs to enhance media distribution given the high proportion of this traffic in an operator's network.
- Interest in a system pushing the limits of CDNs towards:
	- Reducing latency for live contents
	- Improving the efficiency (in terms of resources) for the distribution of mid popularity contents
- Several improvement points
	- Remove DNS-related latency
	- More dynamicity of routing following the dynamicity of the caches
	- Enhance type of contents distributed (benefits not only for media, but other contents as well)
	- Adapt delivery to content type
- Adapting content distribution to SBR

### Questions on CDN use case
	- Detailed explanation on latency and middle tier benefits from Luis
	- Dirk elaborate on replica switching benefit, avoiding DNS propagation pbs.
	- Toerless : How are the use cases influencing the solution? Gap with CATS? Question on properties and metrics of service instances used in selection.

## 3/ Web browsing use case for Rosa - Paulo

- Accessing web resources takes a lot of time: DNS / CDN / static content
- Major issues:
	- DNS latency
	- Time to first bit is large due to name resolution time and access to CDNs
	- If resources are distributed, name resolution penalty further increased.
- Expected benefits from Rosa
	- Inband URL to IP mapping reducing page retrieval time
	- Deeper integration of SAG in ISP networks
- No questions from the audience

## 4/ Why current solutions fall short - Dirk

- How is service routing done today?
	- resolving name onto network locator: several issues
		- Distribution
		- Dynamicity
		- Efficiency
	- Service stickiness Vs. stateless anycast mechanisms
	- Service selection based on service policies and metrics, may be different from ISP's
	URLs are not used everywhere
- Desired solution: E2E procedure between a client and the best possible service instance that can serve it
	- How to make routing / assignment decisions at a high rate?
	- How to improve update speed?
	- How to use specific policies for routing / chaining / assignment?
How current solution fall short?
	- DNS: lack dynamicity, adding latency
	- CATS: computing related metrics, limited to a single domain, tunnelling all the traffic to egress point
	- LISP: latency, lack affinity support, no use of service metrics (yet)
	- ALTO: Static, latency issues
- Expected benefits of a solution
	- Multi-domain
	- Dynamic
	- no dependence on network state

### Questions:
	- Toerless: Few years ago, proposals to improve DNS in IETF, based on measurements.
	- Why does look-up delay matter?
	Dirk: solution is not a replacement for DNS, complementary system when latency matters.
	- Granularity of using the solution? How to take the decision of using the solution? Dirk: Difference on dynamicity of the scenario
	- How can you make change frequently without requiring the traffic to go through the overlay all the time?
	- what is the scale / type of overl.ay that Rosa is competing with? Dirk: for now, focus on understanding the problem space.

## 5/ Requirements and blueprint for an approach - Dirk

- Key requirements
	- Associate service instances to a single address
	- Announce routes to specific service instances
	- Interconnection between ROSA islands
	- Constraint-based routing capabilities
	- Instance selection on ingress nodes only
	- in band data transfer capability
	- Adhere to affinity towards service instance
	- Optional
		- Mobility
		- Handshake
		- Endpoint integration
- Blueprint overview
	- SARs build a ROSA overlay
	- Overlay without the use of tunnels?
	- Push-based protocol
- Main message flow
	- selection of instance <=> change in packet's IP address
- SAR forwarding engines
- Possible encoding of resolution information in the Overlay

### Questions
	- How would it work for a service developer to use the system?
	Dirk: It depends on the deployment scenario. The more deployments, the less friction in the use of the system.
	- Dirk: Are we addressing a concrete problem people have? How can we continue discussion about the solution?
	For application developers to use ROSA, it needs to be usable day one, without requiring them to do something too specific.
	- Interesting topic, potential latency gains but very complex given that application developers want simple solutions.
	- Can you guarantee zero packet loss? Maybe use case from this.
