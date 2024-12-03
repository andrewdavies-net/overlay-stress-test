### builds pipeline twice
no cache only shared-workspace between tasks, emptydir /var/lib/containers. This runs the build pipeline twice once to build, next time entire container file
> Around 7 mins 

### build-and-deploy-standard-build-twice--layers
using --layers to cache the build images to local & remote repository, emptydir /var/lib/containers 
> Around 30 mins (didnt read cache correctly either)
### build-and-deploy-standard-build-twice-block-rwo
Using cephblockfs behind /var/lib/containers, build didnt appear to pickup cache or previous layers 
> Around 17 mins 

### build-and-deploy-standard-build-twice-file-rwx
Using ceph rwx file volume behind /var/lib/containers, build didnt appear to pickup cache or previous layers 
> Around 1 hour 20 mins (No average of runs as it took too long)

### oci-shared-workspace
Using emptydir for /var/lib/containers, exporting early common stage tar of containerfile and pushing into shared-workspace hosted on a pvc (dont think it matters what), next tekton task reimports tar into buildah/tags/references as next stage
> Around 6 mins 4 seconds 