Community Shared BOSH Releases
==============================

This project references BOSH release tarballs from across the BOSH community.

Additionally, it allows BOSH release tarballs to be uploaded to a shared blobstore. This is useful for BOSH releases that are not already sharing their tarballs (for example, core Cloud Foundry projects `cf` and `cf-mysq`).

Releases
--------

- **admin-ui** [v2](https://github.com/cloudfoundry-community/admin-ui-boshrelease/tree/v2) (20M), [v3](https://github.com/cloudfoundry-community/admin-ui-boshrelease/tree/v3) (20M)

```
bosh upload release https://admin-ui-boshrelease.s3.amazonaws.com/boshrelease-admin-ui-3.tgz
```

- **cf** [v170](https://github.com/cloudfoundry/cf-release/tree/v170) (1.5G), [v173](https://github.com/cloudfoundry/cf-release/tree/v173) (2.5G)

```
bosh upload release https://community-shared-boshreleases.s3.amazonaws.com/boshrelease-cf-170.tgz
bosh upload release https://community-shared-boshreleases.s3.amazonaws.com/boshrelease-cf-173.tgz
```

- **cf-mysql** [v8](https://github.com/cloudfoundry/cf-mysql-release/tree/v8) (118M), [2014-06-30](https://github.com/cloudfoundry/cf-mysql-release/tree/96aadfd72c77028bf682a18d79b3c5836d48b341) (241M)

```
# v8
bosh upload release https://community-shared-boshreleases.s3.amazonaws.com/boshrelease-cf-mysql-8.tgz
# dev release 2014-06-30
bosh upload release https://community-shared-boshreleases.s3.amazonaws.com/boshrelease-cf-mysql-8%2Bdev.1.tgz
```

- **cf-services-contrib** [v5](https://github.com/cloudfoundry-community/cf-services-contrib-release/tree/v5) (795.7M)

```
bosh upload release https://cf-contrib.s3.amazonaws.com/boshrelease-cf-services-contrib-5.tgz
```

- **cf-riak-cs** [v2](https://github.com/cloudfoundry-incubator/cf-riak-cs-release/tree/v2) (196.8M)

```
bosh upload release https://community-shared-boshreleases.s3.amazonaws.com/boshrelease-cf-riak-cs-2.tgz
```

- **consul** [v4](https://github.com/cloudfoundry-community/consul-boshrelease/tree/v4) (61.5M)

```
bosh upload release https://consul-boshrelease.s3.amazonaws.com/boshrelease-consul-4.tgz
```

- **docker** [v4](https://github.com/cf-platform-eng/docker-boshrelease/tree/v4) (32M)

```
bosh upload release https://community-shared-boshreleases.s3.amazonaws.com/boshrelease-docker-4.tgz
```

- **docker-registry** [v1](https://github.com/cloudfoundry-community/docker-registry-boshrelease/tree/v1) (32M)

```
bosh upload release https://docker-registry-boshrelease.s3.amazonaws.com/boshrelease-docker-registry-1.tgz
```

- **mesos** [v1](https://github.com/cf-platform-eng/shipyard-boshrelease/tree/v1) (384.9M)

```
bosh upload release https://mesos-boshrelease.s3.amazonaws.com/boshrelease-mesos-1.tgz
```

- **redis** [v5](https://github.com/cloudfoundry-community/redis-boshrelease/tree/v5) (1M)

```
bosh upload release https://redis-boshrelease.s3.amazonaws.com/boshrelease-redis-5.tgz
```

- **shipyard** [v3](https://github.com/cf-platform-eng/shipyard-boshrelease/tree/v3) (6.1M)

```
bosh upload release https://shipyard-boshrelease.s3.amazonaws.com/boshrelease-shipyard-3.tgz
```

- **sslproxy** [v5](https://github.com/cloudfoundry-community/sslproxy-boshrelease/tree/v5) (2.4M)

```
bosh upload release https://sslproxy-boshrelease.s3.amazonaws.com/boshrelease-sslproxy-5.tgz
```

Follow the version links above for deployment manifest/spiff template examples.

Usage
-----

```
bosh upload release URL
```

Adding releases
---------------

Most projects' owners can upload their own BOSH release tarballs using `bosh share releases` from the `bosh-gen` project. If a project owner is not sharing tarballs, such as cf-release and cf-mysql-release, then they can be shared using this project.

For example, with cf-release:

```
$ cd path/to/cf-release
$ bosh create release --with-tarball releases/cf-173.yml
```

This creates `releases/cf-173.tgz`.

Change back to this `community-shared-boshreleases` project:

```
$ cd ../community-shared-boshreleases
$ bosh share release ../cf-release/releases/cf-173.tgz
...
https://community-shared-boshreleases.s3.amazonaws.com/boshrelease-cf-173.tgz
```

The resulting URL can now be added to the `README.md` above.

One time only, please email [Dr Nic Williams](mailto:&#x64;&#x72;&#x6E;&#x69;&#x63;&#x77;&#x69;&#x6C;&#x6C;&#x69;&#x61;&#x6D;&#x73;&#x40;&#x67;&#x6D;&#x61;&#x69;&#x6C;&#x2E;&#x63;&#x6F;&#x6D;) and he will set you up with access:

- Read/write credentials to the AWS S3 account for your BOSH release blobstores/buckets

When he gives you the AWS S3 credentials, place them in `config/private.yml` of this project:

```yaml
---
blobstore:
  s3:
    access_key_id:     ACCESS
    secret_access_key: SECRET
```

Finally, so they are useful for other `bosh-gen` projects, place them in the `~/.fog` file and you'll easily be able to reuse them for each new BOSH release:

```yaml
:community:
  :aws_access_key_id:     ACCESS
  :aws_secret_access_key: SECRET
```
