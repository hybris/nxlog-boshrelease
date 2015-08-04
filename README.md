BOSH release to run nxlog
=======================

Background
----------

### What is nxlog?

In concept NXLog is similar to syslog-ng or rsyslog but it is not limited to unix and syslog only. It supports different platforms, log sources and formats so nxlog can be an ideal choice to implement a centralized logging system.

Usage
-----

To use this bosh release, first upload it to your bosh:

```
bosh upload release https://github.com/hybris/nxlog-boshrelease
```

For [bosh-lite](https://github.com/cloudfoundry/bosh-lite), you can quickly create a deployment manifest & deploy a cluster:

```
templates/make_manifest warden
bosh -n deploy
```

For AWS EC2, create a single VM:

```
templates/make_manifest aws-ec2
bosh -n deploy
```

### Override security groups

For AWS & Openstack, the default deployment assumes there is a `default` security group. If you wish to use a different security group(s) then you can pass in additional configuration when running `make_manifest` above.

Create a file `my-networking.yml`:

```yaml
---
networks:
  - name: nxlog1
    type: dynamic
    cloud_properties:
      security_groups:
        - nxlog
```

Where `- nxlog` means you wish to use an existing security group called `nxlog`.

You now suffix this file path to the `make_manifest` command:

```
templates/make_manifest openstack-nova my-networking.yml
bosh -n deploy
```
