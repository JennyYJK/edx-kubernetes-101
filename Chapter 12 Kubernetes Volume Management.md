# Chapter 12 Kubernetes Volume Management
## Volumes
When container is restarted, old data is not restored.
Volume is a directory backed by a storage medium.
![](Chapter%2012%20Kubernetes%20Volume%20Management/Screen%20Shot%202019-09-01%20at%203.22.35%20PM.png)
Volume is attached to a Pod (same lifespan) and allows data to be preserved across containers in the pod.

## Volume Types
	- emptyDir
		- created for the Pod as soon as it is scheduled on the worker node
		- contents deleted forever when Pod is terminated
	- hostPath
		- share a directory from the host to the Pod
		- persistent even when Pod is terminated (on the host)
	- gcePersistentDisk/awsElasticBlockStore/azureDisk/azureFile
	- cephfs
		- existing CephFS volume can be mounted
		- when Pod terminates, volume is unmounted and contents are preserved
	- nfs/iscsi
		- mount NFS/iSCSI share into a Pod
	- secret
		- for sensitive information
	- configMap
		- provide configuration data, shell commands, and arguments
	- persistentVolumeClaim
		- attach a PersistentVolume

## PersistentVolumes
	- PersistentVolume (PV) subsystem provides APIs for users and admins to manage and consume persistent storage
	- PersistentVolumeClaim API resource type to consume the Volume
![](Chapter%2012%20Kubernetes%20Volume%20Management/Screen%20Shot%202019-09-01%20at%2011.15.09%20PM.png)
	- PersistentVolumes can be dynamically provisioned based on the StorageClass resource
	- StorageClass contains pre-defined provisioners and params to create a PersistentVolume
	- Using PersistentVolumeClaims, a user sends the request for dynamic PV creation, which gets wired to the StorageClass resource

## PersistentVolumeClaims
	- Request for storage by a user
	- Based on type, access mode, and size
	- Three access modes
		- ReadWriteOnce: read-write by a single node
		- ReadOnlyMany: read-only by many nodes
		- ReadWriteMany: read-write by many nodes
![](Chapter%2012%20Kubernetes%20Volume%20Management/Screen%20Shot%202019-09-01%20at%2011.20.46%20PM.png)
	- Once a suitable PersistentVolume is found, it is bound to a PersistentVolumeClaim
![](Chapter%2012%20Kubernetes%20Volume%20Management/Screen%20Shot%202019-09-01%20at%2011.45.12%20PM.png)
	- After a successful bound, the PersistentVolumeClaim resource can be used in a Pod
	- Attached PersistentVolumes can be released for it to be reclaimed, deleted, or recycled for future usage (data deleted)

	- Container Storage Interface (CSI) is standardized in order to work on different container orchestrators for managing external storage like Volumes



#pivotal