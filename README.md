# BOSH Release for mariadb (Incomplete, Development in progress)

## Using this BOSH release

To upload the latest final release to your BOSH:

```
git clone https://github.com/drnic/mariadb-boshrelease.git
cd mariadb-boshrelease
bosh upload release releases/mariadb-1.yml
```

For [bosh-lite](https://github.com/cloudfoundry/bosh-lite), you can quickly create a deployment manifest:

```
cp examples/bosh-lite-cluster.yml local-cluster.yml
sed -i '' -e "s/DIRECTOR_UUID/$(bosh status | grep UUID | awk '{print $2}')/" local-cluster.yml
bosh deployment local-cluster.yml
bosh -n deploy
```
