## Create the build

```
oc new-build --name simple-rdkit --strategy=docker https://github.com/OpenRiskNet/jupyter-notebook-images.git --context-dir=simple-rdkit
```

## JupyterHub configuration

```
    {
        'display_name': 'RDKit (Ubuntu 18.04 / Python 3.7)',
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
