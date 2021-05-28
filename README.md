Hive requires a ClusterImageSet which points to an ocp-release image for running an OpenShift installation  
via the [installer](https://github.com/openshift/installer).  

You can further understand the purpose of release images [here](https://github.com/openshift/installer/blob/master/docs/dev/alternative_release_image_sources.md).  

This binary pulls the latest x86_64 image references from quay.io, stores them in a csv,  
pushes the contents to a Google Sheet, creates a ClusterImageSet in the hive namespace for each,  
and populates the Google Form for lab requests with the image name.

Building quickly on local machine:  
docker run --rm -v "$PWD":/usr/src/sync-cluster-imagesets -w /usr/src/sync-cluster-imagesets golang:alpine go build -o build/sync-cluster-imagesets -v

A Dockerfile exists in build directory:
cd build  
docker build -t {registry_url}:{registry_port}/{registry_namespace}/sync-cluster-imagesets .

We use a floating tag - latest - to push but you should always use a digest (sha:abi67d9f...) when deploying the image.
