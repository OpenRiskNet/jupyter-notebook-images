# Jupyter Notebook Images

This repo contains definitions of Jupyter notebook images for deploying to an OpenRiskNet Virtual Environment (VE).
Instructions for deploying Jupyter to an ORN VE can be found
[here](https://github.com/OpenRiskNet/home/tree/master/openshift/deployments/jupyter).

Typically each sub-directory contains the definitions (e.g. a `Dockerfile`) for a single notebook image.

All images currently are standard Jupyter notebook images that need to run with relaxed OpenShift security specifications.
It is preferable to convert these to s2i builds along the lines found 
[here](https://github.com/jupyter-on-openshift/jupyter-notebooks/tree/master/build-configs).

## Deploying a notebook image to the Jupyter project in an ORN VE

The `simple-rdkit` image is used as an example. Other notebook images should be similar.
You should be able to do this as the `developer` user. All the acton takes place in the `jupyter` project.

## Step 1: Creating the build

From within the `jupyter` project:
```
oc new-build --name simple-rdkit --strategy=docker https://github.com/OpenRiskNet/jupyter-notebook-images.git --context-dir=simple-rdkit
```
Change the name and context-dir parameters if using a different notebook.

This creates a new BuildConfig and starts the build. The container images is built and pushed to the OpenShift registry.
Subsequent changes to the GitHub repo will be detected and the image re-built.

## Step 2: Adding the image to the JupyterHub configuration

Edit the `jupyterhub-cfg` ConfigMap in the `jupyter` project and add the defintion of your image to the `c.KubeSpawner.profile_list`
List. You will add something like this:
```
{
  'display_name': 'Simple RDKit',
  'kubespawner_override': {
    'image_spec': 'simple-rdkit:latest',
    'supplemental_gids': [100],
    'volume_mounts': [
       {
         'name': 'data',
         'mountPath': '/home/jovyan'
       }
    ]
  }
}
```

The `supplemental_gids` parameter is needed because the image needs to run as a predefined goroup ID.
The `volume_mounts` specifies where to mount the user's PVC and needs to be where Jupyter is looking for its notebooks.

## Step 3: Redeploy JuputerHub

Run a new deployment of the `jupyterhub` deployment.
