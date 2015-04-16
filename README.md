# topface.docker_image_checker

Check if image exists in docker registry. Useful if you deploy on marathon with
[topface.marathon_app](https://github.com/Topface/ansible-marathon_app) and
don't want to see ever-failing tasks because image cannot be found.

Note that playbook role assumes that you run local registry behind https.

## Usage

Just put this role before deploying your app:

```yaml
- hosts: marathon-api-server
  gather_facts: no
  roles:
    - role: topface.docker_image_checker
      docker_registry: whatever.corp
      docker_image: myapp
      docker_tag: 1.2.3
    - role: topface.marathon
      marathon_app:
        id: /myproject/myapp
        # the rest is omitted
        # but is using whatever.corp/myapp:1.2.3
```

This would fail if docker image `whatever.corp/myapp:1.2.3` does not exist.
It makes sense to use variable instead of hardcoding `docker_tag`.
Pass it when you run your playbook.

## License

[MIT](LICENSE)
