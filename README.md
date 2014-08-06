# BOSH Release for logstash-shipper

## Usage

To use this bosh release, first upload it to your bosh:

```
bosh target BOSH_HOST
git clone https://stash.hybris.com/idefix/bosh-release-logstash-shipper.git
cd bosh-release-logstash-shipper
bosh upload release releases/logstash-shipper-1.yml
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
