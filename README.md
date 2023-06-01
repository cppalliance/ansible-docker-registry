
## Ansible Docker Registry

Sets up a basic docker registry mirror as a pull through cache.

NOTES:

- Where are images cached?

Refer to this variable in defaults/main.yml:    

```
docker_registry_storage_fs_root_directory_on_host: /data
```

- How should the docker client be configured?  

If auth hasn't been set up, allow insecure-registries. If implementing a full mirror then point to registry-mirrors. Or prepended the cache to the docker command instead: `docker pull mycache:5000/library/postgres:latest`.  It appears the extra library/ path is required for some docker images when pointing to an external registry. However, registry-mirrors solves that.

/etc/docker/daemon.json:  

```
{
  "registry-mirrors": ["https://my-docker-repo-mirror.my.company.com"],
  "insecure-registries":[""https://my-docker-repo-mirror.my.company.com"]
}
```

