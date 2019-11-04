# Chapter 3 Kubernetes
- Container orchestration
	- Automatic bin packing
		- automatically schedules containers based on resource needs and constraints
			- maximizes utilization without sacrificing availability
	- Self healing
		- Failed nodes recovery via health check based on rules/policy
		- Prevents traffic from being routed to unresponsive containers
	- Horizontal scaling
		- Scaled manually/automatically based on CPU or custom metrics
	- Service discovery and load balancing
		- Unique IP per container
		- Single DNS name to a set of containers for LB
	- Automated rollouts and rollbacks
	- Secret and configuration management
		- Manages separately from the container image
	- Storage orchestration
		- Automatically mounts software-defined storage (SDS) solutions
	- Batch execution
- Modular and pluggable architecture
- Functionality can be extended by
	- custom resources
	- operators
	- custom APIs
	- scheduling rules
	- plugins


#kubernetes/edxIntroToKubernetes/chapter3	
#pivotal/flexhour