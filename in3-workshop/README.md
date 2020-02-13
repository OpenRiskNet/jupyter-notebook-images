## Create the build

```
oc new-build --name in3-workshop --strategy=docker https://github.com/OpenRiskNet/jupyter-notebook-images.git --context-dir=in3-workshop
```

## JupyterHub configuration

```
    {
        'display_name': 'IN3 workshop image (Python, R + various libraries)',
        'kubespawner_override': {
            'image_spec': 'in3-workshop:latest',
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
