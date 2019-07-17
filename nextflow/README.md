## Create the build

```
oc new-build --name nextflow --strategy=docker https://github.com/OpenRiskNet/jupyter-notebook-images.git --context-dir=nextflow
```

## JupyterHub configuration

```
    {
        'display_name': 'Nextflow (Ubuntu 18.04 / Java 10)',
        'kubespawner_override': {
            'image_spec': 'nextflow:latest',
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
